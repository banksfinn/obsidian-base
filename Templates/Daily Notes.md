---
tags:
- dailies
created: 
things_to_track: true
can_be_boolean: false
or_a_number: 5
or_a_string: example string (with spaces!)
---
<%*
// Relevant variables to all sections
let recurringTodosFileName = "Bullet Journal/Recurring/Recurring Tasks.md"
let recurringWorkFileName = "Bullet Journal/Recurring/Recurring Work.md"
let relevantDate = moment(tp.file.title).format("dddd")

function grabRecurringTodos(text, tag, date) {
	let todos = []
	let splitText = text.split(date)
	// If we don't show the date, return nothing
	if (!splitText || splitText.length < 2) {
		return todos
	}
	// Grab the second portion (aka after the date), split by double new line
	let relevantSection = splitText[1].split("\n\n")[0] ?? ""
	// Skip the first element
	for (const item of relevantSection.split("\n").slice(1)) {
		todos.push(item.slice(0, 6) + tag + " " + item.slice(6) + "\n")
	}
	return todos
}

// Recurring todos
let recurringTasksFile = tp.file.find_tfile(recurringTodosFileName)
let recurringTasksData = await this.app.vault.read(recurringTasksFile)
let recurringTasks = grabRecurringTodos(recurringTasksData, "#recurring", relevantDate)

// Recurring todos
let recurringWorkFile = tp.file.find_tfile(recurringWorkFileName)
let recurringWorkData = await this.app.vault.read(recurringWorkFile)
let recurringWork = grabRecurringTodos(recurringWorkData, "#recurring", relevantDate)
%>
####           [[<% fileDate = moment(tp.file.title, 'M-D-YYYY').startOf('month').format('MMMM YYYY') %>]]
<< [[<% fileDate = 'Bullet Journal/Daily' + moment(tp.file.title, 'M-D-YYYY').subtract(1, 'd').format('YYYY') + "/" + moment(tp.file.title, 'M-D-YYYY').subtract(1, 'd').format('MMMM') + "/" + moment(tp.file.title, 'M-D-YYYY').subtract(1, 'd').format('M-D-YYYY') %>|Yesterday]] | [[<% fileDate = 'Bullet Journal/Daily' + moment(tp.file.title, 'M-D-YYYY').add(1, 'd').format('YYYY') + "/" + moment(tp.file.title, 'M-D-YYYY').add(1, 'd').format('MMMM') + "/" + moment(tp.file.title, 'M-D-YYYY').add(1, 'd').format('M-D-YYYY') %>|Tomorrow]] >>

# Notes
- 

# To-Do
<%*
if (recurringTasks.length > 0) {
	for (const todo of recurringTasks) {
		tR += todo
	}
} else {
	tR += "- [ ] "
}
%><% tp.file.cursor() %>

<%*
let day = moment(tp.file.title).day()
if (recurringWork.length > 0 || (day !== 6 && day !== 0)) {
	tR += "# Work To Do\n";
	for (const todo of recurringWork) {
		tR += todo
	}
}
%>


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
