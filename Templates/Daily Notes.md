---
tags:
- enter tags here
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