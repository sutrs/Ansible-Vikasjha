# YAML Basics

YAML (YAML Ain't Markup Language) is a human-readable data serialization format. It is often used for configuration files, data exchange between languages with different data structures, and in applications where data is being stored or transmitted.

## Indentation and Structure

YAML uses indentation to represent the structure of data. Spaces are preferred over tabs, and indentation should be consistent. It uses colons and dashes to denote key-value pairs and lists.

## Key-Value Pairs

Key-value pairs are used to represent data. The key and value are separated by a colon, with a space after the colon. For example:

```yaml
name: John Doe
age: 30
```


## Lists
Lists or arrays are represented using a hyphen followed by a space, and items in the list are indented. For example:
```
- item 1
- item 2
- item 3
```

## Nested Structures
You can nest data structures within YAML, including dictionaries within dictionaries and lists within dictionaries. Maintain consistent indentation for nested structures.

```
person:
  name: John Doe
  age: 30
  hobbies:
    - Reading
    - Swimming
```

## Comments
YAML supports comments. Comments begin with the # symbol, and everything to the right of it is treated as a comment.

```
# This is a comment
key: value
```

## Multiline Strings
You can represent multiline strings using the | character for a literal block style. This preserves line breaks and indentation.
```
description: |
  This is a multiline
  string in YAML.
```

## Quoted Strings
If your string contains characters that could be interpreted as a YAML indicator (e.g., :, -, #), you can enclose the string in double or single quotes.
```
message: "This is a string with a colon: it's inside quotes."
```
