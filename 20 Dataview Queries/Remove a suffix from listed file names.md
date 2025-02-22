---
description: Remove a suffix or prefix from a filename delimited with certain characters 
---
#dv/list #dv/link #dv/regexreplace #dv/from 

# Remove a suffix from listed file names

## Basic 

> [!hint]
> If you have another character or character sequence that is delimiting your suffix, you need to exchange the `--` of the regular expressions . Here a few examples:
> If your delimiter is "\_\_" use `regexreplace(file.name, "__.*$", "")`
> If your delimiter is "{" use `regexreplace(file.name, "{.*$", "")`
> If your delimiter is "--!" use `regexreplace(file.name, "--\!.*$", "")`

```dataview
LIST WITHOUT ID link(file.link, regexreplace(file.name, "--.*$", ""))
FROM "10 Example Data/prefixes and suffixes"
```

## Variants

### Replace a prefix instead

> [!hint] Adjusted examples (see callout above): `"^.*__"`, `"^.*{"`, `"^.*--\!"`

```dataview
LIST WITHOUT ID link(file.link, regexreplace(file.name, "^.*_", ""))
FROM "10 Example Data/prefixes and suffixes"
```

### Replace prefix and suffix


```dataview
LIST WITHOUT ID link(file.link, regexreplace(regexreplace(file.name, "^.*_", ""), "--.*$", ""))
FROM "10 Example Data/prefixes and suffixes"
```