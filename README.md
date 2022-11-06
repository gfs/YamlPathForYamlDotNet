# YamlPath Extensions for YamlDotNet
This project adds support for YamlPath queries on YamlDotNet's `YamlNode` objects as a `Query` extension method.

## Usage

### Query
The API for Query is specified like so:
```csharp
/// <summary>
///     Get all the <see cref="YamlNode" /> that match the provided yamlPath query.
///     For YamlPath documentation see 
///         https://github.com/wwkimball/yamlpath/wiki/Segments-of-a-YAML-Path 
///     Does not support Collectors.
/// </summary>
/// <param name="yamlNode">The YamlMappingNode to operate on</param>
/// <param name="yamlPath">The YamlPath query to use</param>
/// <returns>An <see cref="IEnumerable{YamlNode}" /> of the matching nodes</returns>
public static IEnumerable<YamlNode> Query(this YamlNode yamlNode, string yamlPath)
```

Basic Usage to search a whole document:
```csharp
// The extension methods are in this namespace
using gfs.YamlDotNet.YamlPath;

// Your query goes here
string yourYamlPathQuery = "...";

// load yml
YamlStream yaml = new YamlStream();
yaml.Load(new StringReader(targetYamlString));

// get the node you want to query, for example the root node of the first document
YamlMappingNode mapping = (YamlMappingNode)yaml.Documents[0].RootNode;

// Receive an enumeration of nodes which match the YamlPath query
IEnumerable<YamlNode> matching = mapping.Query(yourYamlPathQuery);
```
### Validate your YamlPath
Check your query for errors/unsupported behavior, receiving a human readable list of errors found, or an empty list for no errors:
```csharp
using gfs.YamlDotNet.YamlPath;

string yourYamlPathQuery = "...";

List<string> queryProblems = YamlPathExtensions.GetQueryProblems(yourYamlPathQuery);
```

## Details
Implemented based on the YamlPath Spec located here: https://github.com/wwkimball/yamlpath/wiki/Segments-of-a-YAML-Path

Supported:
[Anchors](https://github.com/wwkimball/yamlpath/wiki/Segment:-Anchors)
[Array Elements](https://github.com/wwkimball/yamlpath/wiki/Segment:-Array-Elements)
[Array Element Searches](https://github.com/wwkimball/yamlpath/wiki/Segment:-Array-Element-Searches)
[Array Slices](https://github.com/wwkimball/yamlpath/wiki/Segment:-Array-Slices)
[Hash Attribute Searches](https://github.com/wwkimball/yamlpath/wiki/Segment:-Hash-Attribute-Searches)
[Hash Keys](https://github.com/wwkimball/yamlpath/wiki/Segment:-Hash-Keys)
[Hash Slices](https://github.com/wwkimball/yamlpath/wiki/Segment:-Hash-Slices)
[Pass-Through Selections for Arrays of Hashes](https://github.com/wwkimball/yamlpath/wiki/Segment:--Array-of-Hashes-Pass-Through-Selection)
[Search Keywords](https://github.com/wwkimball/yamlpath/wiki/Search-Keywords)
[Set Values](https://github.com/wwkimball/yamlpath/wiki/Segment:-Set-Values)
[Wildcard Segments](https://github.com/wwkimball/yamlpath/wiki/Wildcard-Segments)

Not supported:
[Collectors](https://github.com/wwkimball/yamlpath/wiki/Segment:-Collectors)

## Origins
Originally a 2022 Microsoft Hackathon Project to add YamlPath support to [Application Inspector](https://github.com/microsoft/ApplicationInspector/) queries. PR with [Original Implementation](https://github.com/microsoft/ApplicationInspector/pull/509). 

This repository extends and improves that implementation and publishes it as a consumable NuGet package.  This repository and its NuGet packages are not supported or maintained by Microsoft Corporation.

## License
MIT
