---
description: Shows all projects with a finish date that lies in a specific month or year, optionally with additional metadata
---
#dv/table #dv/date #dv/dateformat #dv/from #dv/where #dv/groupby 


> [!hint] Contributed by [Jillard via Discord](https://discord.com/channels/686053708261228577/875721010144477204/1003859143792283658)

# Show projects finished this month

## Basic 

```dataview
Table finished 
FROM "10 Example Data/projects" 
WHERE dateformat(date(finished), "yyyy-MM") = "2022-07"
```

## Variants

### Show additional metadata

```dataview
Table project-id, finished, tags 
FROM "10 Example Data/projects" 
WHERE dateformat(date(finished), "yyyy-MM") = "2022-07"
```

### Show all finished projects grouped by month

```dataview
Table rows.project-id AS "Project ID", rows.finished AS "Finished on", rows.tags AS "Tags" 
FROM "10 Example Data/projects" 
WHERE finished
GROUP BY dateformat(date(finished), "yyyy-MM")
```

### Show all finished projects grouped by month of a specific year

```dataview
Table rows.finished AS "Finished on"
FROM "10 Example Data/projects" 
WHERE finished AND dateformat(date(finished), "yyyy") = "2022"
GROUP BY dateformat(date(finished), "yyyy-MM")
```