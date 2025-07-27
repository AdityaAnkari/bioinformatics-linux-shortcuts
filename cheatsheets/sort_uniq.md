# 🔢 `sort` and `uniq` Cheatsheet for Bioinformatics

## 🧾 What Are `sort` and `uniq`?

- `sort` arranges lines alphabetically or numerically.
- `uniq` removes or counts duplicate lines **(only works on sorted input!)**

Together, they help you clean up lists, summarize counts, and prepare inputs for downstream tools or plots.

---

## 🎯 Why Use These?

| Task | Tool | Why |
|------|------|-----|
| Sort gene names, read IDs, or chromosomes | `sort` | ✅ Alphabetical or numerical order |
| Remove duplicate entries | `uniq` | ✅ Clean inputs |
| Count how many times each value appears | `uniq -c` | ✅ Quick stats |
| Prepare for plotting | `sort | uniq -c` | ✅ Tidy summary |

---

## 🔠 `sort`: Reordering Lines

```bash
# Sort alphabetically (default)
sort genes.txt

# Sort numerically
sort -n expression_levels.txt

# Sort by column 2
sort -k2 file.tsv

# Sort by column 3, numeric
sort -k3,3n file.tsv
```

### 🔍 Common Options

| Option | Description |
|--------|-------------|
| `-n` | Numeric sort (not alphabetical) |
| `-kN` | Sort by column N |
| `-r` | Reverse order |
| `-u` | Unique sort (no duplicates) |

---

## 🚫 `uniq`: Remove Duplicates

⚠️ Input **must be sorted** for `uniq` to work correctly.

```bash
# Remove duplicate lines (must sort first!)
sort genes.txt | uniq

# Count occurrences
sort genes.txt | uniq -c

# Only show duplicates
sort genes.txt | uniq -d

# Show only unique entries (no duplicates)
sort genes.txt | uniq -u
```

---

## 🧬 Bioinformatics Use Cases

```bash
# Count number of times each gene appears in a list
sort gene_hits.txt | uniq -c | sort -nr

# Remove duplicated read IDs from FASTQ headers
zcat reads.fastq.gz | grep "^@" | cut -d " " -f1 | sort | uniq > unique_read_ids.txt

# Summarize number of variants per chromosome
cut -f1 variants.vcf | grep -v "^#" | sort | uniq -c
```

---

## 🧠 Useful Combos

```bash
# Count and sort most common gene names
sort genes.txt | uniq -c | sort -nr | head

# Get unique file extensions
ls | awk -F. '{print $NF}' | sort | uniq
```

---

## ⚠️ Common Pitfalls

| Problem | Fix |
|--------|-----|
| `uniq` doesn’t remove duplicates | Must use `sort` first |
| Output is unordered | Use `sort` with `-k` or `-n` |
| Duplicates with spaces look different | Normalize spacing or use `awk` |
| Too many pipes? | Test each step with `head` or `less` |

---

## ✅ Summary Table

| Goal | Command |
|------|---------|
| Alphabetical sort | `sort file.txt` |
| Numeric sort | `sort -n file.txt` |
| Sort by 2nd column | `sort -k2 file.txt` |
| Remove duplicates | `sort file | uniq` |
| Count duplicates | `sort file | uniq -c` |
| Show only duplicates | `sort file | uniq -d` |

---

## 📘 Final Note

`sort` and `uniq` are deceptively simple but incredibly powerful. They let you **summarize data**, **clean files**, and **prep inputs** for statistical analysis without ever opening a spreadsheet.

Once you master these, you’ll save hours of cleanup and become a better data wrangler.


