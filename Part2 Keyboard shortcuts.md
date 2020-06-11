# Keyboard shortcuts

You could be mad when you just come to Windows from Linux distributions or macOS. Because the shortcuts totally different between here there.

## General

Before turn back to be a ninja, remember the equivalent shortcuts in Windows.

| Function                   | Windows               | Linux Distribution  | macOS            |
| -------------------------- | --------------------- | ------------------- | ---------------- |
| KEY                        | `Ctrl`, `Alt`, `⊞`, - | `Ctrl`, `Alt`, -, - | `⌘`, `⌥`, -, `⌃` |
| Delete right               | `Delete`              | `Ctrl+d`            | `⌃d`             |
| Head of line               | `Home`                | `Ctrl+a`, ahead     | `⌃a`             |
| Tail of line               | `End`                 |                     | `Ctrl+e`, end    | `⌃e` |
| Move cursor by words       | `Ctrl+←/→`            | -                   | -                |
| Delete to the head of line | `Ctrl+Home`           | -                   | -                |
| Delete a word              | `Ctrl+BackSpace`      | `Ctrl+w`            | `⌃w`             |

## Special in Windows Terminal

Windows Terminal is a UWP app and now is V1.0, very easy to use and configure. Recommended.

### split panel

Default:

### close panel

PowerShell: `Ctrl+Shift+w`

Command Line Prompt: -

WSL2 consoles: `Ctrl+D`

### move cursor between panels

`Alt+←/→/↑/↓`

### split panel with different

Custom

## About autocompletion in PowerShell

Unix-style autocomplete lists all candidates when you tab which is straightforward and indicative, but PowerShell's autocomplete is a little be weird, you use TAB to swap candidates.

So how can you make it more unix-like?

Run command `Set-PSReadlineKeyHandler -Key Tab -Function MenuComplete`.

As for add autocompletion to your PowerShell function, this [blog](https://foxdeploy.com/2017/01/13/adding-tab-completion-to-your-powershell-functions/) has a nice introduction.