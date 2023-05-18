---
tags:
- dailies
created: 
things_to_track: true
can_be_boolean: false
or_a_number: 5
or_a_string: example string (with spaces!)
---

####           [[<% fileDate = moment(tp.file.title, 'M-D-YYYY').startOf('month').format('MMMM YYYY') %>]]
<< [[<% fileDate = 'Bullet Journal/Daily' + moment(tp.file.title, 'M-D-YYYY').subtract(1, 'd').format('YYYY') + "/" + moment(tp.file.title, 'M-D-YYYY').subtract(1, 'd').format('MMMM') + "/" + moment(tp.file.title, 'M-D-YYYY').subtract(1, 'd').format('M-D-YYYY') %>|Yesterday]] | [[<% fileDate = 'Bullet Journal/Daily' + moment(tp.file.title, 'M-D-YYYY').add(1, 'd').format('YYYY') + "/" + moment(tp.file.title, 'M-D-YYYY').add(1, 'd').format('MMMM') + "/" + moment(tp.file.title, 'M-D-YYYY').add(1, 'd').format('M-D-YYYY') %>|Tomorrow]] >>

# Notes
- 

# To-Do
- [ ] <% tp.file.cursor() %>


# Work To-Do
- [ ] 


# Meal Tracker
> breakfast::
> lunch:: 
> dinner:: 


# Notes Created
```dataviewjs  
let currentCreated = moment(dv.current().file.name).startOf('day')
let pages = dv.pages().where(p => {
	let fileCreated = moment(p.file.ctime.ts).startOf('day')
	return fileCreated.isSame(currentCreated)
}).filter(p => p.file.path)

if (!pages.length || dv.current().file.name === "Daily Notes Template") {
	dv.header(3, "No notes created today :(")
} else {
	// Group by X
	let groups = pages.groupBy(p => p.file.path.split("/")[1])

	for (let group of groups) {
		dv.table([group.key], group.rows.map(b => [dv.fileLink(b.file.name, false, b.file.name)]))
	}
}
```

# Notes Edited
```dataviewjs  
let currentCreated = moment(dv.current().file.name).startOf('day')
let pages = dv.pages().where(p => {
	let fileCreated = moment(p.file.mtime.ts).startOf('day')
	return fileCreated.isSame(currentCreated)
}).filter(p => p.file.path)

if (!pages.length || dv.current().file.name === "Daily Notes Template") {
	dv.header(3, "No notes edited today :(")
} else {
	// Group by X
	let groups = pages.groupBy(p => p.file.path.split("/")[1])

	for (let group of groups) {
		dv.table([group.key], group.rows.map(b => [dv.fileLink(b.file.name, false, b.file.name)]))
	}
}
```
