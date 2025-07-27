# 🧮 AWK Cheatsheet for Bioinformatics

## 🧾 What Is AWK?

`awk` is a powerful command-line tool for **processing columns of data**. It reads each line of a file, splits it into fields, and lets you print or filter based on those fields.

It’s extremely useful for working with tabular formats like `.tsv`, `.gff`, `.vcf`, `.sam`, and `.bed`.

---

## 🎯 Why Bioinformaticians Use AWK

| You want to... | Can AWK do it? |
|----------------|----------------|
| Print specific columns | ✅ Yes |
| Filter rows by value | ✅ Yes |
| Do math on columns | ✅ Yes |
| Process files line-by-line | ✅ Yes |

---

## 🧪 Basic Syntax

```bash
awk '{print $1}' file.txt
```

- `$1`, `$2`, `$3` → First, second, third columns
- `{print $0}` → Prints entire line
- By default, AWK splits on **spaces or tabs**

---

## 📊 Common Examples

```bash
# Print first column (e.g., read ID or gene name)
awk '{print $1}' file.txt

# Print columns 1 and 3
awk '{print $1, $3}' file.txt

# Only show lines where column 5 > 30 (e.g., MAPQ)
awk '$5 > 30' aln.sam

# Show gene names only if expression > 100
awk '$2 > 100 {print $1}' expression.tsv
```

---

## 🧬 Bioinformatics Use Cases

```bash
# Print chromosome and start position from GFF
awk '{print $1, $4}' annotation.gff

# Filter variants with QUAL > 50
awk '$6 > 50' variants.vcf

# Count how many reads have MAPQ = 60
awk '$5 == 60' aln.sam | wc -l

# Print read name and flag from SAM
awk '{print $1, $2}' aln.sam
```

---

## 🛠️ Field Separator with -F

Use `-F` to change the delimiter, e.g., for CSV or colon-separated files.

```bash
# For CSV (comma-separated)
awk -F',' '{print $1, $2}' genes.csv

# For colon-separated data
awk -F':' '{print $1}' file.txt
```

---

## 💡 Pro Tips

| Need to... | Use This |
|-----------|----------|
| Print multiple columns | `{print $1, $2, $5}` |
| Skip header | `NR > 1` |
| Match exact string | `$3 == "gene"` |
| Match pattern | `$3 ~ /gene/` |
| Exclude pattern | `$3 !~ /intron/` |

---

## ⚠️ Common Pitfalls

| Mistake | Fix |
|--------|-----|
| Spaces in filename | Quote it: `"file name with space.txt"` |
| Mixing tabs and spaces | Use `cat -A file` to inspect |
| File has header | Skip with `NR > 1` |
| Confused between `$1` vs `$0` | `$1` is 1st column, `$0` is full line |

---

## ✅ Summary Table

| Task | Command |
|------|---------|
| Print column 2 | `awk '{print $2}'` |
| Filter rows where col3 > 10 | `awk '$3 > 10'` |
| Print first & last columns | `awk '{print $1, $NF}'` |
| Skip header row | `awk 'NR > 1'` |

---

## 📘 Final Note

Mastering `awk` means mastering column-based text manipulation. In bioinformatics — where every file is a giant table — it’s one of the **most valuable tools in your toolkit**.

Use `awk` to filter, format, and understand your data — without ever opening Excel.

****
