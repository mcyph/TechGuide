# JSON

* JSON stands for JavaScript Object Notation
* The specification was originally created by Douglas Crockford, whose ideas for programming JavaScript as introduced in his book "Javascript the Good Parts" can be seen in his design decisions.
* Supports:&#x20;
  * Objects with string keys and arbitrary values (called hash maps/hash tables or dictionaries in other languages than JavaScript), e.g. `{"My Key 1": ["My Value 1"], "My Key 2": "My Value 2"}`
  * Arrays (called lists in other languages), e.g. `[1, "2", 3.0]`
  * Strings, e.g. `"My String Value"`. Only double quotes, not single quotes/parenthesis.
  * Floating point values e.g. `-55.5`
  * Integers: `55` or `-42`
* Does not support lists, numbers or other types for object (hash table/hash map) keys, only strings.&#x20;
* Does not support comments or trailing commas. See also [https://medium.com/@marycriv/why-json-doesnt-allow-comments-fe93f7106c62](https://medium.com/@marycriv/why-json-doesnt-allow-comments-fe93f7106c62) for why comments were left out of the original specifications.
* Does not support types such as dates; however some parsers have extensions to allow for these kinds of cases.
* Implementations of JSON types in a more compact or more easily seekable machine-readable format are seen in BSON (used by MongoDB) or MessagePack.&#x20;
  * One caveat to note is that although these may be more compact in their basic format than JSON, that these binary formats tend to be less compressible/redundant, which means that when zipped their ratios may be lower than ordinary JSON.&#x20;
