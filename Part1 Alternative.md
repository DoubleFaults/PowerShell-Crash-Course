# What is X in PowerShell

The most questions when you are new to PowerShell are What is mv/which/grep/less/head/tail ... in PowerShell?

## Command in common

### Almost the same

But remember that they are `aliases` to another PowerShell commands. 

PS importing them at the beginning of a session is just for convenience.

> `ls` `cd` `cat` `rm`
> 
> `ps` `ping`
> 
> `echo` `history` `ping`
> 
> `yes`
> 
> `sort`

What does `yes` do

> `yes | rm -i <sth>`

### less

### grep

TOC

### find

TOC

### watch

TOC

### column

One of the most ignored useful command

> What is the point of column
> 
> make list -> table
> 
> `cat /etc/passwd | column -t -s :`

In powershell it is `ft`, format as table

### man, command/which 

## Operator's differences

## Theory

I category them as 4 types, they are the level of how much do the alternatives approach to the origins

**Type I:** PowerShell predefines several same-name commands which also play the same role as they do in *Unix.

**Type II:** Still the same role, some of them may have the similar names in PowerShell but also have a little differences in usage.

**Type III:** Both name and usages are different from each other, but can achieve the same functionality. aka. workaround in PowerShell

**Type VI:** Very difficult to do that in PowerShell.

| in *Unix                                 | Type        | in PowerShell                                                                                                                                                                           |
| ---------------------------------------- | ----------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| ls, cd, cat, rm                          | Type I      | Filesystem cmd                                                                                                                                                                          |
| ps, ping                                 | Type I      | system cmd                                                                                                                                                                              |
| echo, history, ping, yes, column         | Type I      | input/output                                                                                                                                                                            |
| > >> < <br> 1> 2> 3> 4> 5> <br> &> *>    | Type I      | output redirection                                                                                                                                                                      |
| `|`                                      | Type I      | pipeline                                                                                                                                                                                |
| tee                                      | Type II     | tee -Variable/FilePath/..., PowerShell Tee-Object just subscribe the flow <br> but *Unix tee (puts flow to output and)forward (a copy) the flow                                         |
| less                                     | Type II     | Out-Host -Paging                                                                                                                                                                        |
| man                                      | Type II     | Get-Help                                                                                                                                                                                |
| which/command                            | Type II     | Get-Command                                                                                                                                                                             |
| grep                                     | Type II/III | findstr,                                                                                                                                                                                |
| watch                                    | Type III    |                                                                                                                                                                                         |
| function                                 | Type II/III | **Normal functions** almost the same(positional parameter, exit status, but PowerShell support implicit return value) <br> **Advanced function** supports named and pipeline parameters |
| awk, sed, ssh, chown, chmod, uname, sudo | Type VI     |                                                                                                                                                                                         |


// guide lines

cd, pwd, cat(included `cat xx <EOF`), mv, ps, cp, ln, rm, mkdir/rmdir, touch, echo, history, alias, which

pipeline, xargs, head, tail, less, sort, watch, tr

grep, find, awk, sed, tar, rsync, ssh 

locate, man

chown, chmod, df/du, uname

ping, wget/curl, iptables,

kill, init/shutdown/restart, mount, dd

redirect(> )

sudo

## operation

You can do arithmetic calculation like other script language.

### condition

```powershell
if ( $A -and $B) {}; if ( $A -or $B) {};
if (-not $A) {}; if (! $false) {}; 
```

```powershell
if ( $A -eq $B) {}; if ( $A -ne $B) {};
if ( $A -gt $B) {}; if ( $A -lt $B) {};
if ( $A -ge $B) {}; if ( $A -le $B) {};
```

```powershell
if ("PowerShell" -like "*shell"){}; if ("PowerShell" -notlike "*bash"){};
if ("PowerShell" -match "^Power"){}; if ("PowerShell" -notmatch ".*sh$"){};
if ("PowerShell" -contains "she"){}; if ("PowerShell" -notcontains "they"){};
```

```powershell
if (7 -in @(1,2,3,5,7,11)){}; if (9 -notin @(1,2,3,5,7,11)){};
```
[ref: operator](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_operators?view=powershell-7)