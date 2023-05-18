---
tags:
- monthly
created: <% tp.file.creation_date() %>
---
<% tp.file.rename(moment(tp.file.title).format('MMMM YYYY')) %>
<< [[<% fileDate = moment(tp.file.title).subtract(1, "month").startOf("month").format('MMMM YYYY') %>|Previous Month]] | [[<% fileDate = moment(tp.file.title).add(1, "month").startOf("month").format('MMMM YYYY') %>|Next Month]] >>

# Active List
```dataviewjs
let minDate = moment(dv.current().file.name).startOf("month")
let maxDate = moment(dv.current().file.name).endOf("month")

let relevantPages = dv.pages('#dailies').where(p => p.file.name !== "Daily Notes Template" && moment(p.file.name) >= minDate && moment(p.file.name) <= maxDate)

let uncompletedTasks = relevantPages.file.tasks.where(t => !t.completed && t.text)

let groupedTasks = uncompletedTasks.groupBy(t => dv.fileLink(t.path))
let sortedGroupedTasks = groupedTasks.sort(t => moment(t.key.path.split('/').slice(-1)[0].slice(0, -3)).valueOf())

dv.taskList(sortedGroupedTasks)

```

# [[Habit Tracker]]

```dataviewjs  
let minDate = moment(dv.current().file.name).startOf("month")
let maxDate = moment(dv.current().file.name).endOf("month")

// get all journal pages for this month  
let pages = dv.pages('#dailies').where(p => moment(p.file.name) >= minDate && moment(p.file.name) <= maxDate) 

// Sort
pages.values.sort((a, b) =>  {
return moment(a.file.name).diff(moment(b.file.name))
})

dv.table(["Date"], pages.map(page => [dv.fileLink(page.file.name, false, moment(page.file.name).format("M-D-YYYY"))]))
```


# Life Events
- 