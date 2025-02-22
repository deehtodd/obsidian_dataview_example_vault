---
description: Show multiple meta data fields in one table column - useful when you need to take renamed fields into account
---
#dv/table #dv/from #dv/where #dv/flatten #dv/filter

# Show two metadatas in same table column

## Basic 

```dataview
TABLE wake-up, [go-to-sleep, gotosleep] as "Bed time", [lunch, dinner] AS "Meal times"
from "10 Example Data/dailys"
where date(day).weekyear = 3
```

## Variants

In case you only have one valid value per file for this column that is stored in different meta data fields, use filter and flatten:

```dataview
TABLE wake-up, ST AS "Bed time", [lunch, dinner] AS "Meal times"
from "10 Example Data/dailys"
where date(day).weekyear = 3
FLATTEN filter([gotosleep, go-to-sleep], (x) => x) as ST
```