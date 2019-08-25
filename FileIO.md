
# Async

Pretty much everything has an `async` version.



# Administration

* `File.Delete(path)`
* `File.Move(source, destination)`
* `File.Copy(source, destination)`
* `File.Exists(path)`



# Encrypt

Encrypts a file so that only the current account can decrypt it.

* `File.Encrypt/Decrypt(path)`


# Reading / Writing

* `File.Create`
* `File.Open`
* `File.WriteAll(Bytes/Lines/Text)`
* `File.AppendAll(Bytes/Lines/Text)`
* `File.ReadAll(Bytes/Lines/Text)`



## Examples


```csharp
File.WriteAllLines("myFile.txt", theText, Encoding.UTF8);
File.AppendAllLines("myFile.txt", moreText, Encoding.UTF8);
var myText = await File.ReadAllLinesAsync("myFile.txt");
```

```csharp
using(StreamWriter sw = new StreamWriter("myFile.txt"))
{
    sw.WriteLines("Hello\nWorld")
}
```





# Directories

* `DirectoryInfo(path)`
    * `FullName`
    * `Parent`
    * `Name`
* `Directory.Create/Delete/Move`
* `Directory.EnumerateFiles/Directories`


# Path

* `Path.GetFullPath(path)`
* `Path.GetFileName(path)`
* `Path.GetExtension(path)`
* `Path.GetDirectory(path)`
* `Path.Combine(string[] paths)`    or  `Path.Combine(path1, path2)`

### Temp
* `Path.GetTempFileName()`    Create temporary file and return path
* `Path.GetTempPath()`        Get %TEMP% folder