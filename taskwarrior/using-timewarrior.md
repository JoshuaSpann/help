# Using the Warriors: <small>Time Warrior</small>

## Invoke
`timew`

## Start Tracking TIme
`timew start`

## Stop Tracking Time
`timew stop`

## Track Time with Tag
`timew start` *`tagValue`*
`timew stop` *`tagValue`*

## Show All Time Summary Reports
`timew summary` *[`tagValue`]*

## Integrate TimeWarrior with TaskWarrior
`timew` installs a script that you need to copy to the `task` hooks dir:

`cp /usr/share/doc/timew/ext/on-modify.timewarrior ~/.task/hooks && chmod +x ~/.task/hooks/on-modify.timewarrior`
