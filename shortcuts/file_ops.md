# 🛠️ Linux File Operations for Bioinformatics

This guide covers essential Linux commands for creating, copying, moving, renaming, deleting, and inspecting files and folders.  
These operations are **daily tasks** in any bioinformatics project — whether you're downloading FASTQ files, moving genome assemblies, or organizing results.

---

## 📄 Creating and Inspecting Files

| Command | Description |
|--------|-------------|
| `touch file.txt` | Create a new empty file |
| `mkdir folder_name` | Make a new directory |
| `stat filename` | View size, modification time, and permissions |
| `file filename` | Show file type (text, gzip, FASTQ, etc.) |
| `wc -l filename` | Count the number of lines (e.g., reads in `.fastq`) |
| `head filename` | Show first 10 lines |
| `tail filename` | Show last 10 lines |

---

## 📁 Copying and Moving Files

| Command | What it Does |
|--------|----------------|
| `cp file1 file2` | Copy file1 to file2 |
| `cp file.txt folder/` | Copy to a folder |
| `cp -r dir1/ dir2/` | Copy a folder and its contents |
| `mv file new_name` | Rename a file |
| `mv file /path/to/folder/` | Move file to another directory |
| `mv *.fastq.gz raw_data/` | Move multiple files at once |

---

## ❌ Deleting Files and Folders

| Command | Caution |
|--------|---------|
| `rm file.txt` | Delete file |
| `rm *.html` | Delete all `.html` files in the folder |
| `rm -r folder/` | Delete folder and everything inside |
| `rm -rf folder/` | Force delete without prompt ⚠️ |

💡 **Warning:** `rm -rf` is powerful and dangerous. Always double-check the path before using it.

---

## 📏 Checking File Size

| Command | Use |
|--------|-----|
| `du -sh file` | Show human-readable size of file |
| `du -sh folder/` | Show size of a folder |
| `ls -lh` | Show file sizes in a list |
| `du -sh *` | See sizes of all items in current directory |

---

## 🔍 Examples from Bioinformatics Work

| Task | Command |
|------|---------|
| Create folder for QC reports | `mkdir results/qc` |
| Copy genome to shared folder | `cp -r genomes/arabidopsis/ shared/refs/` |
| Move trimmed files into folder | `mv *.trimmed.fastq.gz trimmed_reads/` |
| Check size of raw reads | `du -sh data/raw_reads/` |
| Count reads in a file | `wc -l sample1.fastq.gz` *(use with `zcat` for compressed)* |

---

## 💡 Pro Tips

- Use **Tab** to autocomplete file and folder names
- Use **wildcards** like `*.fastq`, `*_R1.fastq.gz` to select groups of files
- Use `history | grep cp` to see your past copy commands
- Use `stat` and `ls -lt` to track modified files

---

## ✅ Summary

| You Want To… | Use This |
|--------------|----------|
| Create files/folders | `touch`, `mkdir` |
| Copy or move files | `cp`, `mv` |
| Rename something | `mv old new` |
| Delete files/folders | `rm`, `rm -r` |
| View file size | `du -sh`, `ls -lh` |
| See file type or info | `file`, `stat` |

---

📘 Organizing your files is half the battle in bioinformatics.  
Use these tools to keep your workspace tidy, reproducible, and analysis-ready!

