---
description: Calculate the sum of multiple times (hh:mm), i.e. the sum of hours one has spent on a project 
---
#dv/dataviewjs #dvjs/pages #dvjs/mutate #dvjs/table #dvjs/map #dvjs/luxon #dvjs/sort

# Calculate Sum of working hours for a project

## Basic 

```dataviewjs
const projects = dv.pages('"10 Example Data/projects"')
	.mutate(p => p.workHourSum = sumUpWorkHours(p["working hours"]))


dv.table(["Project", "Working Hours", "Sum Working Hours"], 
		 projects.map(p => [p.file.link, p["working hours"], p.workHourSum]))

function sumUpWorkHours(workingHours) {
	const durations = workingHours
		.split(",")
		.map(h => dv.luxon.Duration.fromISOTime(h.trim()));
	
	const sum = durations.reduce((acc, curr) => acc + curr, 0)
	return dv.luxon.Duration.fromMillis(sum) 
}
```

## Variants

### Format sum output and output more metadata
> [!info] Possible formats
> Have a look at the [luxon documentation](https://moment.github.io/luxon/api-docs/index.html#durationtoformat) for a reference of possible formats

```dataviewjs
const projects = dv.pages('"10 Example Data/projects"')
	.mutate(p => p.workHourSum = sumUpWorkHours(p["working hours"]))
	.sort(p => p.status, "desc")


dv.table(["Project", "ID", "Status", "Tags", "Sum"], 
		 projects.map(p => [p.file.link, p["Project ID"], p.status, p["tags"], p.workHourSum]))

function sumUpWorkHours(workingHours) {
	const durations = workingHours
		.split(",")
		.map(h => dv.luxon.Duration.fromISOTime(h.trim()));
	
	const sum = durations.reduce((acc, curr) => acc + curr, 0)
	return dv.luxon.Duration.fromMillis(sum).toFormat("hh'h' mm'm'")
}
```