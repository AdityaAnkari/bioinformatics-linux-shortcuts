# 🧪 Essential Data Processing Commands for Bioinformatics

## 🧾 What Is This?

This guide introduces you to key Linux command-line tools used for **text and tabular data manipulation**, especially for handling formats like FASTQ, SAM, GFF, and VCF in bioinformatics.

Understanding tools like `cut`, `sort`, `uniq`, `paste`, `tr`, `head`, `tail`, and `wc` helps you efficiently extract and filter data  without using Excel or writing long scripts.

---

## 🎯 Who Is This For?

| You are... | Is this for you? |
|------------|------------------|
| Working with `.txt`, `.tsv`, `.csv`, `.vcf`, `.gff`, `.sam`, `.fastq` | ✅ Definitely |
| Copying and pasting between Excel and text files | ❗Please stop and read this |
| Wanting to count reads, extract columns, sort data | ✅ Yes |
| Building pipelines or doing preprocessing | ✅ Absolutely |

---

## ✂️ `cut` — Extract Columns by Delimiter

Extract fields (columns) from tabular data (like GFF, CSV, or SAM).

### Syntax

```bash
cut -f <fields> -d <delimiter> <file>
```

### Examples

```bash
# Extract gene IDs from 9th column of GFF
cut -f9 -d$'\t' annotation.gff

# Get read name and MAPQ score from SAM file (columns 1 and 5)
cut -f1,5 aln.sam
```

---

## 📊 `sort` — Sort Lines Alphabetically or Numerically

### Syntax

```bash
sort <file>
sort -k <column> -n <file>  # Sort numerically by column
```

### Examples

```bash
# Sort a list of gene names
sort genes.txt

# Sort a tab-separated file by 3rd column numerically
sort -k3,3 -n -t$'\t' expression.tsv
```

---

## 🔁 `uniq` — Remove Duplicate Lines

Often used after `sort`.

### Syntax

```bash
uniq <file>
sort <file> | uniq
```

### Examples

```bash
# Unique read IDs
cut -f1 aln.sam | sort | uniq > unique_reads.txt
```

---

## ➕ `paste` — Merge Files Side by Side

### Syntax

```bash
paste file1 file2
```

### Examples

```bash
# Combine gene names and expression values
paste genes.txt expression.txt > combined.tsv
```

---

## 🔤 `tr` — Translate or Delete Characters

Useful for replacing or removing characters.

### Syntax

```bash
tr <set1> <set2>
```

### Examples

```bash
# Replace tabs with commas
cat file.tsv | tr '\t' ',' > file.csv

# Remove carriage return characters (from Windows files)
tr -d '\r' < win_file.txt > clean_file.txt
```

---

## 🔢 `wc` — Count Lines, Words, Bytes

### Syntax

```bash
wc -l   # Lines
wc -w   # Words
wc -c   # Bytes
```

### Examples

```bash
# Count number of reads in FASTQ (each read = 4 lines)
zcat sample.fastq.gz | wc -l

# Count number of variants in VCF
grep -v "^#" variants.vcf | wc -l
```

---

## 🔽 `head` and `tail` — Preview Top/Bottom Lines

Useful for checking file format or sampling.

### Syntax

```bash
head -n 10 file
tail -n 10 file
```

### Examples

```bash
# View first few lines of SAM
head aln.sam

# View last 5 entries in a log file
tail -n 5 log.txt
```

---

## 🧬 Real Bioinformatics Examples

```bash
# Extract chromosome names from BAM header
samtools view -H aln.bam | grep "@SQ" | cut -f2 | cut -d: -f2

# Count unique read IDs from a FASTQ
zcat sample.fastq.gz | grep "^@" | cut -d ' ' -f1 | sort | uniq | wc -l

# Combine gene names and expression counts into one file
paste gene_ids.txt counts.txt > gene_counts.tsv
```

---

## ⚠️ Common Mistakes

| Mistake | Fix |
|--------|-----|
| Forgetting to sort before `uniq` | Always `sort | uniq` |
| Wrong delimiter in `cut` or `sort` | Use `-d$'\t'` for tabs |
| Using `cut` on inconsistent columns | Check file structure with `head` first |
| Assuming `wc -l` gives read count | Divide by 4 for FASTQ |

---

## ✅ Summary

| Goal | Command |
|------|---------|
| Extract columns | `cut -f1,3` |
| Sort data | `sort -k2,2n` |
| Remove duplicates | `sort | uniq` |
| Join files side-by-side | `paste` |
| Replace characters | `tr '\t' ','` |
| Count lines/reads | `wc -l` |
| Preview data | `head`, `tail` |

---

## 📘 Final Note

These tools are essential for anyone working with biological data. They let you rapidly inspect, reshape, and clean massive files on the command line — all without needing to load anything into R, Python, or Excel.

Keep this page handy as your go-to reference for processing bioinformatics files efficiently.

