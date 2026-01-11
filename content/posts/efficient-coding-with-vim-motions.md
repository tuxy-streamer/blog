---
title: "Efficient coding with vim motions."
description: "Explore how Vim motions enable lightning-fast code navigation and editing. Master the fundamental motion commands, text objects, and operator combinations to streamline your workflow and boost coding productivity."
date: 2026-01-09T14:20:38+05:30
Categories: ["Productivity", "Code Editor", "Vim"]
tags: ["vim motions", "efficiency", "navigation"]
draft: false
---

When you hear vim is the best text editor, it isn't the performance or
the customizability of the editor. Most of the time it's about the vim motions.

## What are vim motions ?

Vim motions are the commands used to navigate your cursor from one place
of the file to another.
It is kind of a language in itself using which you can describe the edits
you want to make inside the current opened file.
It isn't bound only to the Vim editor but can be installed as an extension
on your preferred code editor.

## Why use vim motions ?

- Helps keep your hands on the keyboard and not constantly reach the mouse for navigation
  which prevents hand fatigue.
- Helps to make editing faster and fluid without much thinking.
- Makes code navigation easier with searching.
- Makes typing and coding fun.

## How can you use vim motions in your code editor ?

[Vim Keybindings Everywhere - The Ultimate List](https://github.com/erikw/vim-keybindings-everywhere-the-ultimate-list?tab=readme-ov-file#ides)

## Modality of vim

Vim is a modal editor, that means there are different modes which can be used
to interact with the text in the editor.
There are 13 modes but most of the time you'll be using these 5 modes.

1. Normal Mode:
   - Default mode for navigation, copy, cut and paste etc.
2. Insert Mode:
   - Mode to insert text.
3. Visual Mode
   - Mode to select text.
4. Command Line Mode:
   - Mode to run commands.
5. Terminal Mode
   - Mode to open a terminal.

## Normal Mode: Navigation

- **Navigation**: Moving cursor in text.
- **Motion**: Key used to move the cursor.

You start by default in this mode but if you switched mode then
you can press `ESC` key to exit the current mode and switch it to normal mode.

### Basics

**Character wise**:
(Arrow keys equivalent)

| Motion | Action |
| :----: | :----: |
|  `j`   |  Down  |
|  `k`   |   Up   |
|  `h`   |  Left  |
|  `l`   | Right  |

#### Horizontal motion

- **word**: A word consists of a sequence of letters, digits and underscores,
  or a sequence of other non-blank characters, separated with white space (spaces,
  tabs, EOL (End Of Line)).
  > [!NOTE]
  > An empty line is also considered to be a word.
- **WORD**: A WORD consists of a sequence of non-blank characters,
  separated with white space.
  > [!NOTE]
  > An empty line is also considered to be a WORD.

1. Word wise:

   | Motion | Action                                   | Scope | Direction |
   | :----: | :--------------------------------------- | :---: | :-------: |
   |  `w`   | Move to first character of next word     | word  |   Right   |
   |  `e`   | Move to last character of next word      | word  |   Right   |
   |  `b`   | Move to first character of previous word | word  |   Left    |
   |  `W`   | Move to first character of next WORD     | WORD  |   Right   |
   |  `E`   | Move to last character of next WORD      | WORD  |   Right   |
   |  `B`   | Move to first character of previous WORD | WORD  |   Left    |

2. Line Border wise:

   | Motion | Action                                              | Direction |
   | :----: | :-------------------------------------------------- | :-------: |
   |  `$`   | Move to last character of the line                  |   Right   |
   |  `0`   | Move to first character of the line                 |   Left    |
   |  `g_`  | Move to last non white-space character of the line  |   Right   |
   |  `^`   | Move to first non white-space character of the line |   Left    |

3. Character searching

   |  Motion   | Action                                         | Direction |
   | :-------: | :--------------------------------------------- | :-------: |
   | `f<char>` | Move to next `<char>` you type                 |   Right   |
   | `t<char>` | Move to just before next `<char>` you type     |   Right   |
   | `F<char>` | Move to previous `<char>` you type             |   Left    |
   | `T<char>` | Move to just before previous `<char>` you type |   Left    |

After doing a character search using the above motion,
you can go for next search character or the previous search character using:

- `'` (Single Quote Key) for next `<char>`.
- `,` (Comma Key) for previous `<char>`.

> [!NOTE]
> These two work like the next and previous buttons when you do a normal search

#### Vertical motion

1. Page wise:

   | Motion | Action                 | Direction |
   | :----: | :--------------------- | :-------: |
   |  `G`   | Move to the first line |    Up     |
   |  `gg`  | Move to the last line  |   Down    |

2. Block wise / Paragraph wise:

**Paragraph**: A paragraph begins after each empty line and consists of
contiguous lines until the next empty line.

> [!NOTE]
> A blank line (only containing white space) is not a paragraph

| Motion | Action                                   | Direction |
| :----: | :--------------------------------------- | :-------: |
|  `{`   | Move to the first character of paragraph |    Up     |
|  `}`   | Move to the last character of paragraph  |   Down    |

## Insert Mode: Text insertion

This mode allows to insert text.
Use `Esc` to get back to normal mode after inserting text.

| Shortcut | Action                                        | Scope | Direction |
| :------: | :-------------------------------------------- | :---: | :-------: |
|   `i`    | Insert text before the position of the cursor | Char  |   Left    |
|   `a`    | Insert text after the position of the cursor  | Char  |   Right   |
|   `I`    | Insert text at the start of the line          | Line  |   Left    |
|   `A`    | Insert text at the end of the line            | Line  |   Right   |
|   `o`    | Insert text on a new line above the cursor    | Line  |   Down    |
|   `O`    | Insert text on a new line below the cursor    | Line  |    Up     |

## Visual Mode: Text Selection

This is a mode where you can select text.
Use `Esc` to get back to normal mode after inserting text.

|  Shortcut  | Action                                                  | Scope |
| :--------: | :------------------------------------------------------ | :---: |
|    `v`     | Select by using motions from current position of cursor | Char  |
|    `V`     | Select by using motions from current line of cursor     | Line  |
| `Ctrl + v` | Select text like a block by using motions               | Block |

## Command Line Mode

This mode helps to run commands.

|    Shortcut    | Action                                   |
| :------------: | :--------------------------------------- |
| `:<commands>`  | Run editor `<commands>`                  |
|  `/<keyword>`  | Search a `<keyword>` in the current file |
| `:!<commands>` | Run shell `<commands>`                   |

During search mode, you can use

- `n` to go to the next `<keyword>`.
- `N` to go the previous `<keyword>`.
  > [!NOTE]
  > These two work like the next and previous buttons when you do a normal search

## Terminal Mode

This mode gives you access to a terminal with the local shell environment you have.
To activate this mode you have to enter command mode and then type:
`:te`, `:ter`,`:term`,`:termi`, `:termin`, `:termina`, `:terminal` any one of these.
Your editor will change into terminal and if you want to exit the terminal mode
then you have to close your terminal normally with the `exit` command.
