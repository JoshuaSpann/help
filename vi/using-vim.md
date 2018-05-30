# Using Vim
---


# Navigation
**Left, Down, Up, Right:**  
`h`, `j`, `k`, `l`

**Forward, Backward 1 Paragraph:**  
`}`, `{`

**Top, Middle, Bottom of Screen:**  
`H`, `M`, `L`

**Top of File, Bottom of File:**  
`gg`, `G`

**Page Down, Page Up:**  
`^f`, `^b`

**Scroll Screen Top to Cursor's Line:**  
`zt`

**Center Screen on Cursor Line:**  
`zz`

**Scroll Screen Bottom to Cursor's Line:**  
`zb`


---

# Indentation
**Caret Brackets:**  
`>` indents  
`<` removes indent


---

# Special Characters
To insert special characters, go into insert mode first, ***prepend all commands with: `<c-k>`***

**C with cedilla (ç):**  
`c,`

**A with grave, ageiu, umlaut:**
`a'`, `a``, `a:`


---

# Special Auto-Completions
**General Text:**  
`^n`

### INSERT Mode Commands Commands
Append all of the following commands with `^x`
**Filename Completion:**  
`^f`

**Dictionary Completion:**  
`^k`

**Whole-Line Completion:**  
`^l`

**Keyword Completion:**  
`^n`

**Command-Line Completion:**  
`^v`

**Scrolling Insert:**  
`^e` or `^y`


---

# Tag Completion
Go to definition with Ctrl-[
Jump Back with Ctrl-t

## Cetting Tag Completion Only for Code
Go into insert mode then press Ctrl-x:

`i`, `^x`

## Get File Completion
`^x` then `^f`

## Insert at End of File


# Insert at Beginning of File


---

# Visual Mode

**Init in Character, Line, Block-wise:**  
`v`, `V`, `<c-v>`

**select word, scentence, paragraph:**  
`aw`, `as`, `ap`


---

# RESOURCES #
https://whileimautomaton.net/2008/11/vimm3/operator
