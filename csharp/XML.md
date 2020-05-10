# Write to XML
```csharp
var theAnimal = new Animal();
using(Stream s = ...)
{
    var serializer = new XmlSerializer(typeof(Animal));
    serializer.Serialize(s, theAnimal);
}
```

# Read from XML
```csharp
Animal theAnimal;
using(Stream s = ...)
{
    var deserializer = new XmlSerializer(typeof(Animal));
    theAnimal = (Animal)deserializer.Deserialize(s);
}
```


# Standard Serialization

Binary serialization : generally avoid because of security concerns


```csharp
class Animal : ISerializable
{
    // public read/write properties, and fields are serialized
    public string Name { get; set; }
    public string Species { get; set; }
    public double Age;


    // Not Serialized
    string Mood { get; set; }               // non-public properties
    public string Nickname { get; }         // Read-only public properties
    public byte this[int i] => array[i];    // Indexers

}
```

# Customizing Serialization


### With `IXmlSerializable`

```csharp
class Animal : IXmlSerializable
{
    public string Name { get; set; }
    public string Species { get; set; }
    public double Age { get; set; }

    public XmlSchema GetSchema() => null;
    public void ReadXml(XmlReader reader)
    {
        reader.ReadStartElement();
        (Name, Species, Age) = // Custom deserialization logic
        reader.ReadEndElement();
    }
    public void WriteXml(XmlWriter writer)
    {
        writer.WriteString(...) //Custom serialization logic
    }

}
```

### With `ISerializable`

```csharp
class Animal : ISerializable
{
    public string Name { get; set; }
    public string Species { get; set; }
    public double Age { get; set; }

    // For Serialization, part of ISerializable
    public void GetObjectData(SerializationInfo info, StreamingContext context)
    {
        info.AddValue("Name",       Name,       typeof(string));
        info.AddValue("Species",    Species,    typeof(string));
        info.AddValue("Age",        Age,        typeof(double));
    }

    // For Deserialization, note: this is not part of ISerializable
    public Animal(SerializationInfo info, StreamingContext context)
    {
        Name =      (string) info.GetValue("Name",      typeof(string));
        Species =   (string) info.GetValue("Species",   typeof(string));
        Age =       (double) info.GetValue("Age",       typeof(double));
    }

}
```



# LINQ to XML

This is useful because not only is it terse, but it separates concerns between the class we are serializing and the serialization logic.

```csharp

XDocument doc = XDocument.Load(File.OpenText("bom.xml"));

var myBillOfMaterials = new
{
    version = doc.Element("BOM").Element("version").Value,
    package = doc.Element("BOM").Element("package").Value,
    jobnum = doc.Element("BOM").Element("jobnum").Value,
    units = doc.Element("BOM").Element("units").Value,
    Record = doc.Element("BOM").Elements("Record").Select(el => RecordParse(el))
};

static Part parse(XElement element)
{

    return new Part()
    {
        ID =        int.Parse(element.Attribute("Number").Value),
        Code =      element.Element("description").Value,
        Length =    double.Parse(element.Element("length").Value),
        Weight =    double.Parse(element.Element("weight").Value),
        NCData =    new NCData(element.Element("nc_data").Value)
    }
}

```