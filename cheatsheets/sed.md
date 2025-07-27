# 🧾 `sed` Cheatsheet for Bioinformatics

## 📦 What Is `sed`?

`sed` stands for **stream editor**. It allows you to:
- Search and replace text
- Delete or modify lines
- Edit files without opening them

`sed` works line-by-line and is great for automating file cleanup, especially in `.fastq`, `.gff`, `.vcf`, `.csv`, and `.txt` files.

---

## 🎯 Why Use `sed` in Bioinformatics?

| You want to... | Is `sed` helpful? |
|----------------|-------------------|
| Clean up FASTQ headers | ✅ Yes |
| Replace or remove specific strings | ✅ Absolutely |
| Fix broken formatting in big files | ✅ Definitely |
| Delete lines or patterns | ✅ 100% |

---

## 🔠 Basic Syntax

```bash
sed 's/find/replace/' file
```

- `s` = substitute
- `find` = pattern to match
- `replace` = what to insert
- By default, affects only first match in each line

---

## 🔄 Replace Text Examples

```bash
# Replace "chr" with "Chr"
sed 's/chr/Chr/' genes.txt

# Replace ALL occurrences per line (add `g`)
sed 's/chr/Chr/g' genes.txt

# Change tabs to commas
sed 's/\t/,/g' file.tsv > file.csv

# Remove quotes
sed 's/"//g' data.txt
```

---

## ❌ Delete Lines or Patterns

```bash
# Delete empty lines
sed '/^$/d' file.txt

# Delete lines starting with #
sed '/^#/d' file.vcf

# Delete lines containing "scaffold"
sed '/scaffold/d' annotation.gff
```

---

## 🧪 Bioinformatics Use Cases

```bash
# Clean FASTQ headers: remove everything after first space
zcat reads.fastq.gz | sed 's/ .*//' > cleaned.fastq

# Fix chromosome names in GFF
sed 's/chr/Chr/g' annotation.gff > new_annotation.gff

# Remove all comment lines from a VCF
sed '/^#/d' variants.vcf > variants.noheader.vcf

# Delete all unmapped reads from SAM (flag 4 as a string match)
sed '/\t4\t/d' aln.sam > mapped_only.sam
```

---

## 📝 In-Place Editing with `-i`

```bash
# Replace text directly in the file
sed -i 's/old/new/g' file.txt

# On macOS, use:
sed -i '' 's/old/new/g' file.txt
```

---

## 💡 Advanced Tricks

```bash
# Replace only on specific line numbers
sed '10s/foo/bar/' file.txt

# Replace only in a line range (lines 5–10)
sed '5,10s/foo/bar/' file.txt

# Add a prefix to each line
sed 's/^/PREFIX_/' file.txt
```

---

## ⚠️ Common Pitfalls

| Problem | Fix |
|--------|-----|
| Nothing changed | Use `-i` or redirect output |
| Replaces only first match | Use `/g` at the end: `s/foo/bar/g` |
| Works differently on macOS | Use `sed -i ''` |
| Special characters (slashes, ampersands) break command | Escape them: `\/`, `\&` |

---

## ✅ Summary Table

| Goal | Command |
|------|---------|
| Replace `A` with `B` | `sed 's/A/B/' file` |
| Replace all `A`s | `sed 's/A/B/g'` |
| Delete empty lines | `sed '/^$/d'` |
| Remove lines with `#` | `sed '/^#/d'` |
| Edit in place | `sed -i 's/x/y/g' file.txt` |

---

## 📘 Final Note

`sed` is one of those tools that can seem magical once you get it. It’s perfect for **editing huge files**, doing **quick cleanup**, and **prepping data** without opening a text editor.

Pair it with `awk`, `grep`, and `cut`, and you’ve got a command-line superpower.


