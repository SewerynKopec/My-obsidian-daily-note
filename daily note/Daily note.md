# Everyday tasks

- [ ] Take meds
- [ ] Meditate
- [ ] Go out for a walk
- [ ] [[Excercise]]
# Tasks due today
```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts == dv.date('today').ts)
.sort(t => t.due), false)
```
# Tasks overdue
```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts < dv.date('today').ts)
.sort(t => t.due), false)
```
# Tasks due in a week
```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts >= dv.date('tomorrow').ts)
.where(t => t.due.ts <= dv.date('today').plus({ weeks: 1 }).ts)
.sort(t => t.due), false)
```
# Tasks due in a month
```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts > dv.date('today').plus({ weeks: 1 }).ts)
.where(t => t.due.ts <= dv.date('today').plus({ month: 1 }).ts)
.sort(t => t.due), false)
```
# Log

- [ ] 
# Tasks completed today
```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => t.completed)
.where(t => t.completion?.ts == dv.date('today').ts)
.sort(t => t.due), false)
```