# What is X in PowerShell

## Command in common

### Almost the same

They are the most famous commands and used at the highest frequency in Shell, PowerShell also gets them by default.

- `ls` `cd` `pwd`
- `rm` `rmdir`
- `echo` `cat` `more`
- `ps` `ping`
- `zip`
- `sort`
- `history`(also `ctrl+r`)
- `yes`

BTW, What does `yes` do

> `yes | rm -i <sth>` # say yes for you


> But do remember that they are `aliases` to PowerShell commands.

## Commands have equivalences

### touch

`touch` creates a empty file in current working directory.

In PowerShell, it is

```powershell
New-Item -ItemType file <filename>
```

it can also be done by

```powershell
$null > filename
```

### head & tail

In fact, `cat` in PowerShell is `Get-Content`.

It can also used to `head` and `tail`

`Get-Content -TotalCount 10 <file>` == `head <file>`

`Get-Content -Tail 10 <file>` == `tail <file>`

`Get-Content -Tail 10 -Wait <file>` == `tail -f <file>`

### for

Basic loop command,

In PowerShell, the usages are

#### classic - C style

```powershell
for(($i=5),($j=10) ; $i -eq $j ; ($i++), ($j--)){
    "`$i=$i"
    "`$j=$j"
}
```

#### functional - forEach

```powershell

$arr = "Power!".ToCharArray()

forEach ($c in $arr) {
    echo "$c"
}

# % is the alias to ForEach-Object
"Power!".tochararray() | % {$_}

# forEach Object can have multiple process and begin/end blocks
"Power!".tochararray() | % {$i=1}{echo "$i $_"}{$i++}{echo "the end"}

```

### if-else

Conditional branches,

In PowerShell, the usage is

```powershell
if (1 -gt 2) {
    "panic"
} else {
    "correct"
}
# 3-operand
$msg = authorized?"Access":"Forbidden"
```

### grep

`grep` is one of the most famous command in Shell for search text, it is short for `global search with regex and print`, originally a `ed`(whose successor is `sed`) command `g/re/p`.

In PowerShell, they are

#### Select-String

From pipeline:

`Select-String -Pattern <regex>`

From files:

`Select-String -Path <wildcard> -Pattern <regex>`

#### Where

grep by properties

`Where <Property> -like "regex"`

> `?` is the alias to `Where-Object`

### find

`find` searches a path for targets.

In PowerShell, it is `Get-ChildItem`

```powershell
$res = Get-ChildItem -Path <path-to-search> -Recursive -Include <wildcard> -File -Exclude <wildcard-split-by-comma>

# filter by date
$res | ? {$_.LastWriteTime -gt $(Get-Date).AddDays(-1)}
```

### less

`less` is advanced version of `more`.

Although we have `<cmdlet> | more` in PowerShell, it can't display anything until cmdlet finished.

so, for `less`, in PowerShell, it is

`Out-Host -Paging`

```powershell
cat <large txt> | Out-Host -Paging
```

### xargs

`xargs` convert output from pipeline to next command's parameter

In PowerShell, it usually achieve by a new way, `forEach-Object`. It can not only handle single output, but iterate array-like output.

1,2,3 | %{ & "script path or scriptBlock" $_}

If you'd like to regard input as a whole array, wrap your array with an outside array, such as `,@(1,2,3)`

### watch

`watch` repeats command and print the output for you periodically.

In PowerShell, Not easy to get it.

When you get familiar with `Function`, you can write a `watch` for yourself.

> Hint:
> In every x sec(default x is 2) ->
> 1. print watching command; 
> 1. run it; 
> 1. clear screen

### man

man can print the manual of the command for you,

In PowerShell, it is `Get-Help`

`Get-Help %`

`Get-Help ?`

### command/which

`command` and `which` can test command if is valid.

In PowerShell, it is

`Get-Command`

`Get-Command ps`

What's more, since all things are object in PowerShell.

There should be a way to inspect an object. It is

`Get-Member`

### tee

`tee` dispatches pipelines to 2 direction, one is handled by tee, the other keeps going.

In PowerShell, `tee` is the alias to `Tee-Object`, it supports to copy pipeline to a file or a variable.

```powershell
ps | tee -LiteralPath C:\Users\akira\ps.log | ft
```

### alias

`alias` is magic.

In PowerShell, it is a set of operations.

`New-Alias`

```powershell
New-Alias -Name ^ -Value Tee-Object
```

`Get-Alias`

```powershell
Get-Alias -Name <wildcard>
Get-Alias -Definition Tee-Object
```

`Set-Alias`

```powershell
# it also can create a new alias

Set-Alias -Name myCat -Value Get-Item

# more parameters for Set-Alias, refer to `Get-Help set-alias`
```

`Import-Alias` `Export-Alias` load and store aliases from files.

### column

One of the most ignored useful command in Shell

> What is the point of column
> 
> make list -> table
> 
> `cat /etc/passwd | column -t -s :`

In powershell, it is `Format-Table` and fortunately `ft` is well-known and widely used.

## Appendix

### operation

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

### Theory

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
| > >> <br> < <br> &>                      | Type I      | output redirection, in PowerShell, outputs are more than 2, <br> 1> 2> 3> 4> 5> 6> <br> &> *> <br> 3: Warning;4: Verbose; 5: Debug; 6: Information                                      |
| `|`                                      | Type I      | pipeline                                                                                                                                                                                |
| tee                                      | Type II     | tee -Variable/-FilePath/...                                                                                                                                                             |
| less                                     | Type II     | Out-Host -Paging                                                                                                                                                                        |
| man                                      | Type II     | Get-Help                                                                                                                                                                                |
| which/command                            | Type II     | Get-Command                                                                                                                                                                             |
| grep                                     | Type II/III | findstr, select-string, where-object                                                                                                                                                    |
| watch                                    | Type III    |                                                                                                                                                                                         |
| function                                 | Type II/III | **Normal functions** almost the same(positional parameter, exit status, but PowerShell support implicit return value) <br> **Advanced function** supports named and pipeline parameters |
| awk, sed, ssh, chown, chmod, uname, sudo | Type VI     |                                                                                                                                                                                         |

> **famous commands**
> 
> cd, pwd, cat(included `cat xx <EOF`), mv, ps, cp, ln, rm, mkdir/rmdir, touch, echo, history, alias, which
> 
> pipeline, xargs, head, tail, less, sort, watch, tr
> 
> grep, find, awk, sed, tar, rsync, ssh 
> 
> locate, man
> 
> chown, chmod, df/du, uname
> 
> ping, wget/curl, iptables,
> 
> kill, init/shutdown/restart, mount, dd
> 
> sudo
