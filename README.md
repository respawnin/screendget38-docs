# Screendget Macropad User Guide (CLI + HID Key Macros)

This guide explains how to use the macro system built into your macropad.  
A *macro* is a stored script that can type text, press keys, hold modifiers, and insert delays.
You can create, edit, and run these macros through the command-line interface (CLI).

<img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/screendget-combi.png?raw=true" alt="screendget38 macropad combination" width="50%" height="50%">


For hardware / combination specific documentations (eg. Setting as master/node, or adjusting RGB LED colours, refer to the [hardware guide here](https://github.com/respawnin/screendget38-docs/blob/main/MacroPad-Hardware-Guide.md).

# **Contents**
1. [Macro Slots](#1-macro-slots)
2. [CLI Commands](#2-cli-commands)
3. [Macro Language Overview](#3-macro-language-overview)
4. [Modifier Keys](#4-modifier-keys)
5. [Supported Named Keys](#5-supported-named-keys)
6. [Explicit Key Actions](#6-explicit-key-actions)
7. [Delays](#7-delays)
8. [Newline and Whitespace Rules](#8-newline-and-whitespace-rules)
9. [Recommended Usage Pattern](#9-recommended-usage-pattern)
10. [Troubleshooting](#10-troubleshooting)
11. [Example Macros (Explained)](#11-example-macros-explained)
12. [Macro Cheat Sheet](#12-macro-cheat-sheet)
13. [Step-by-Step Tutorial](#13-step-by-step-tutorial)

---


# 1) Macro Slots
Your macropad provides **6 macro slots**, indexed:
```
0, 1, 2, 3, 4, 5
```
The slot index follows the following key positions on your macropad:

<img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/macropad_index.png?raw=true" alt="macropad index reference" width="30%" height=auto>

Each slot can hold up to **three** scripts:

- **Tap** macro  
  `macro <slot> <script>`

- **Down** macro (runs on press)  
  `macroD <slot> <script>`

- **Up** macro (runs on release)  
  `macroU <slot> <script>`

Tip: Most users put their main action in **Down** and clear **Up** to avoid accidental double-triggering.

---

# 2) CLI Commands

### Show current macros
```text
macro?
```

### Assign a Tap macro

```text
macro <slot> <script>
```

### Assign a Down macro

```text
macroD <slot> <script>

```

### Assign an Up macro
```text
macroU <slot> <script>
```

### Clear a macro
```text
macro <slot> none
```

----------

# 3) Macro Language Overview

A macro is composed of:

### Plain text

Typed literally:

```
hello world
```

### Tags

Anything inside `<...>` is a command:

```
<enter>
<ctrl>
<-ctrl>
<delay:200>
<tap:f5>

```

Malformed tags stop execution, so ensure every `<` has a matching `>`.

----------

# 4) Modifier Keys

### Hold modifiers
```
<ctrl>
<shift>
<alt>
<gui>   (also <win> or <meta>)

```

### Release modifiers
```
<-ctrl>
<-shift>
<-alt>
<-gui>

```

### Example — Ctrl+C

```
<ctrl>c<-ctrl>
```

### Batch modifier syntax

```
<mods:ctrl+shift>
<mods:>   ← clears all modifiers
```

----------

# 5) Supported Named Keys

### Common keys

```
<enter> <ret> <esc> <tab> <bksp> <backspace> <space>

```

### Arrows

```
<up> <down> <left> <right>
```

### Function keys

```
<f1> ... <f24>
```

These act as tap keys (press+release).

----------

# 6) Explicit Key Actions

```
<tap:NAME>
<down:NAME>
<up:NAME>
```

Where `NAME` is a supported key or a raw keycode.

----------

# 7) Delays

Insert timing pauses:

```
<delay:MS>
```

Useful for UI automation (apps, menus, browser navigation).

----------

# 8) Newline and Whitespace Rules

-   Space = types normally
    
-   `\n` or `\r` = Enter
    
-   `\t` in plain text = ignored (use `<tab>`)
    

----------

# 9) Recommended Usage Pattern

To prevent double-triggering:

```
macroD 0 <ctrl>c<-ctrl>
macroU 0 none
```

----------

# 10) Troubleshooting

**Characters missing?**  
Add:
```
<delay:100>
```

**Terminal copy not working?**  
Use:
```
<mods:ctrl+shift>c<mods:>
```

**Modifier stuck?**  
Ensure your macro releases it explicitly.

----------

# 11) Example Macros (Explained)


### Slot examples:

<img src="https://github.com/respawnin/screendget38-docs/blob/main/imgs/macropad_index.png?raw=true" alt="macropad index reference" width="30%" height=auto>

**Slot 0 – Types “hello”**

```
macro 0 hello
```

**Slot 1 – `help` + Enter**

```
macro 1 help<enter>
```

**Slot 2 – Ctrl+C (recommended clean form)**

```
macro 2 <ctrl>c<-ctrl>
```

**Slot 5 – Full workflow: open Edge, load Gmail**

```
<win><-win><delay:50>edge<delay:150><enter><delay:150>www.gmail.com<delay:150><enter>
```

Users can modify any slot by running:

```
macro <slot> <script>
```

----------

# 12) Macro Cheat Sheet

### Slot Management

```
macro?
macro <slot> <script>
macroD <slot> <script>
macroU <slot> <script>
macro <slot> none
```

### Modifiers

```
<ctrl> <shift> <alt> <gui>
<-ctrl> <-shift> <-alt> <-gui>
<mods:ctrl+shift>
<mods:>
```

### Keys

```
<enter> <esc> <tab> <bksp> <space>
<up> <down> <left> <right>
<f1> ... <f24>
```

### Actions

```
<tap:NAME>
<down:NAME>
<up:NAME>
```

### Delay

```
<delay:MS>

```

----------

# 13) Step-by-Step Tutorial
** Write Your First Macro**

## 1) Check existing macros
```
macro?
```
## 2) Create a simple macro

Make slot 0 type “hello” + Enter:

```
macro 0 hello<enter>
```

## 3) Add key combinations

Set slot 1 to Ctrl+C:

```
macro 1 <ctrl>c<-ctrl>
```

## 4) Add delays for UI timing

Launch Notepad:

```
macro 2 <win><-win><delay:150>notepad<enter>
```

## 5) Build full workflows

Open Chrome → YouTube:

```
macro 3 <win><-win><delay:100>chrome<enter>
<delay:300>youtube.com<enter>
```

## 6) Use Down/Up for one-shot actions

```
macroD 4 help<enter>
macroU 4 none
```

## 7) Clear a macro

```
macro 0 none
```

----------

You’re now fully equipped to use, customize, and extend the macropad macro system.  
Have fun building automations!


