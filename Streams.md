# `Stream`

Provides a generic view of a sequence of bytes. Abstract class.

* ReadByte
* ReadBytes
* WriteByte
* WriteBytes




# `StreamReader` / `StreamWriter`

Can be used on any stream type: (`FileStream`, `MemoryStream`, `TcpClient.GetStream()`)

```csharp
using (StreamWriter sw = File.CreateText("myFile.txt"))
{
    sw.Write("This is a random sentence\n");        // Doesn't automatically add a \n
    sw.WriteLine("This is another sentence");       // Does add a \n
}

using (StreamReader sr = File.OpenText("myFile.txt"))
{
    var theFirstLine = sr.ReadLine();   // "This is a random sentence"
    var theRest = await sr.ReadToEndAsync();
}


```


# `FileStream`
* sync / async
* read / write
* subclasses `Stream`


# `BinaryReader` / `BinaryWriter`

* ReadByte / ReadBytes
* ReadChar / ReadChars
* Read(Int16/Int32/Int64/SByte/Single/String/UInt16/UInt32/UInt64)

# `StringReader` / `StringWriter`

* Uses a `StringBuilder` as the backing store
* Not a stream.

# `MemoryStream`

Uses memory as the backing store


# `TextReader` / `TextWriter`

An abstract class, `StringReader` / `StringWriter` implement this.