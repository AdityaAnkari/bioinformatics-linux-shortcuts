# 🧭 Linux Navigation Commands for Bioinformatics

Navigating the Linux filesystem efficiently is the foundation of bioinformatics work. This cheatsheet teaches you how to move between directories, list contents, access recent paths, and use shortcuts that save time when handling large genomic datasets.

---

## 📂 Basic Directory Movement

| Command | What it Does |
|--------|----------------|
| `pwd` | Show your current working directory |
| `cd foldername` | Move into a subfolder |
| `cd ..` | Move one level up |
| `cd ~` | Go to your home directory |
| `cd -` | Switch to the previous directory |

---

## 🗂️ Listing Files and Folders

| Command | Use Case |
|--------|----------|
| `ls` | List files in current directory |
| `ls -l` | Long list format (shows permissions, size, date) |
| `ls -lh` | Human-readable file sizes (e.g., 3.1G, 55M) |
| `ls -a` | Show hidden files (those starting with `.`) |
| `ls -lt` | List files sorted by modification time |

### Example:
```bash
ls -lh data/
---
## 🌲 Visualizing Folder Structures

| Command     | Use Case                                                                |
| ----------- | ----------------------------------------------------------------------- |
| `tree`      | Show folder structure like a tree (install via `sudo apt install tree`) |
| `tree -L 2` | Show 2 levels of depth                                                  |
| `tree -d`   | Show only directories                                                   |

## 🔁 Directory Stack (pushd/popd)
These help when jumping between two directories repeatedly:
```bash
pushd /mnt/hdd/projectA
# work...
popd  # returns to original directory

## 🕹️ Keyboard Shortcuts to Navigate Faster

| Shortcut   | Action                                                 |
| ---------- | ------------------------------------------------------ |
| `Tab`      | Autocomplete folder/file names                         |
| `Ctrl + R` | Search command history (type part of old command)      |
| `Ctrl + A` | Move to beginning of the line                          |
| `Ctrl + E` | Move to end of the line                                |
| `!!`       | Repeat last command                                    |
| `!fastqc`  | Run the most recent command that started with `fastqc` |

## 📦 Bonus: Bookmark Frequent Paths (using aliases)
Add to your .bashrc or .zshrc:

```bash

alias goT2T="cd ~/projects/T2T-genome"
alias goRaw="cd ~/data/raw_fastq/"

Now you can just type goT2T to jump to your working directory.

## ✅ Summary
| You Want To…        | Use This                         |
| ------------------- | -------------------------------- |
| Move around folders | `cd`, `pwd`, `cd ..`, `cd -`     |
| List files clearly  | `ls -lh`, `ls -a`, `tree`        |
| Save time           | Use Tab, `!!`, `Ctrl+R`, `alias` |
| Switch back/forth   | `pushd`, `popd`, `cd -`          |

## 📘 Mastering these basic commands will make everything else — from alignment to assembly — faster and easier.




