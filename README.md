# YamlPath Extensions for YamlDotNet
This project adds support for YamlPath queries on YamlDotNet's `YamlNode` objects as a `Query` extension method.

Originally implemented as a Microsoft Hackathon Project to add YamlPath support to [Application Inspector](https://github.com/microsoft/ApplicationInspector/) queries. [Original Implementation](https://github.com/microsoft/ApplicationInspector/pull/509).

Basic Usage to search a whole document:

```csharp
using YamlDotNet.YamlPath;

// load yml
YamlStream yaml = new YamlStream();
yaml.Load(new StringReader(targetYamlString));

// get the node you want to query, for example the root node of the first document
YamlMappingNode mapping = (YamlMappingNode)yaml.Documents[0].RootNode;

// Receive an enumeration of nodes which match the YamlPath query
IEnumerable<YamlNode> matching = mapping.Query(yourYamlPathQuery);
```

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

