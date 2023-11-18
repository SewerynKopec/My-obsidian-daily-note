# Description

This is my daily note template for my Obsidian vault. 

I was inspired by [Nicole van der Hoeven's youtube guide](https://www.youtube.com/watch?v=ccN5vJzXwvo) and added my own touches.

I use this note as a task organiser. It helps me manage all the tasks based on their due dates.

## The plugins I use for the note:
- [Tasks](https://github.com/obsidian-tasks-group/obsidian-tasks) - it adds quick add dates for tasks that you can sort by.
- [Dataview](https://github.com/blacksmithgu/obsidian-dataview) - dataviewjs to be exact, remember to enable JavaScript Queries!
- [Calendar](https://github.com/liamcain/obsidian-calendar-plugin)(optional) - adds a calendar witdget for easy access to all the daily notes.

The comment free version is available in the repository.


# Template body:

## Everyday tasks

*Tasks here are hardoceded, so that they appear in every note*

- [ ] Take meds
- [ ] Meditate
- [ ] Go out for a walk
- [ ] [[Excercise]]
## Tasks due today

*Task due today are displayed dynamically. They gather tasks across all of the notes in the "Daily" directory. If your daily notes are in a different dir, change the name accordingly. The tasks are selected by compliton state, the due date is matching with the today's date and sorted by the earliest.*

```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts == dv.date('today').ts)
.sort(t => t.due), false)
```
## Tasks overdue

*The second table is about all the overdue tasks, so I can immedietaly see what I have forgotten from the previous days.*

```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts < dv.date('today').ts)
.sort(t => t.due), false)
```
## Tasks due in a week

*Here are all the tasks due till tomorrow or up to 7 days from today.*

```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts >= dv.date('tomorrow').ts)
.where(t => t.due.ts <= dv.date('today').plus({ weeks: 1 }).ts)
.sort(t => t.due), false)
```
## Tasks due in a month

*The same case as tasks due in a week, just different due dates range.*

```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => !t.completed)
.where(t => t.due?.ts > dv.date('today').plus({ weeks: 1 }).ts)
.where(t => t.due.ts <= dv.date('today').plus({ month: 1 }).ts)
.sort(t => t.due), false)
```
## Log

*Here is the section to write your tasks. Remember to write the due date so it can be searched by the queries.*

- [ ] 

## Tasks completed today

*Today's completed tasks, nothing specific here.*

```dataviewjs
dv.taskList(dv.pages('"Daily"').file.tasks 
.where(t => t.completed)
.where(t => t.completion?.ts == dv.date('today').ts)
.sort(t => t.due), false)
```