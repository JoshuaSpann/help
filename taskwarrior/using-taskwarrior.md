# Using the Warriors: <small>Task Warrior</small>

## Main Command
Invoke taskwarrior with the command: `task`

## Add Task
`task add` *`mytaskname`*

## Display / List Tasks
`task list`

## Set task Due Date
`task modify` *`taskNumber`*  `due:`*`YYYY-MM-DD`*

## Complete a Task

`task` *`taskNumber`* `done`


## Create Project to Hold Tasks
To create with a new task:  
```shell
$  task add "Task Name" project:NewProject
Created task 2.
The project 'NewProject' has changed. Project 'NewProject' is 0% complete (1 task remaining).
```

To add to an existing task:  
```shell
$  task 1 modify project:NewProject
Modifying task 1.
Modified 1 task.
The project 'NewProject' has changed. Project 'NewProject' is 0% complete (2 of 2 tasks remaining).
```


## Track Task with Time Warrior
```shell
$  task TaskName start
$  task TaskName stop
```
