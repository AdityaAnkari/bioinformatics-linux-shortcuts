# 🔍 `grep` Cheatsheet for Bioinformatics

## 📘 What Is `grep`?

`grep` is a command-line tool that **searches for text patterns** inside files. It's super fast and perfect for exploring large genomics files like FASTQ, SAM, GFF, or VCF.

Think of `grep` as “**find rows that contain X**”  whether X is a gene name, chromosome, or read ID.

---

## 🎯 Why Use `grep` in Bioinformatics?

| You want to... | Is `grep` helpful? |
|----------------|-------------------|
| Search for gene names in annotation files | ✅ Yes |
| Filter variants based on pattern | ✅ Absolutely |
| Look for specific reads or chromosomes | ✅ Definitely |
| Remove comments or empty lines | ✅ 100% |

---

## 🔤 Basic Syntax

```bash
grep "pattern" file.txt
```

- Searches for `"pattern"` in each line
- Prints matching lines

---

## 🔬 Common Examples

```bash
# Find lines with "BRCA1"
grep "BRCA1" genes.txt

# Search for chromosome 1 in VCF
grep "chr1" variants.vcf

# Search case-insensitively
grep -i "gene" annotation.gff

# Show line numbers
grep -n "transcript" annotation.gff
```

---

## 🧬 Real Bioinformatics Use Cases

```bash
# Get all variants on chrX
grep "chrX" variants.vcf

# Extract header lines (VCF, GFF, SAM)
grep "^#" file.vcf

# Get reads with "N" in the sequence (ambiguous base)
grep "^@" sample.fastq.gz | grep "N"

# Find genes with "kinase" in GFF
grep "kinase" annotation.gff
```

---

## 🧹 Invert Match or Exclude Lines

```bash
# Exclude comment lines from VCF
grep -v "^#" variants.vcf

# Remove all lines containing "scaffold"
grep -v "scaffold" annotation.gff
```

---

## 🧪 Regular Expressions

```bash
# Lines starting with "AT"
grep "^AT" sequences.txt

# Lines ending in "gene"
grep "gene$" file.txt

# Match either 'CDS' or 'exon'
grep -E "CDS|exon" annotation.gff

# Match exact field with tab delimiter
grep -P "\tgene\t" annotation.gff
```

---

## 💥 Search in Compressed Files

```bash
# With zgrep (grep + gzip)
zgrep "BRCA1" genes.txt.gz

# Pipe from zcat
zcat sample.fastq.gz | grep "^@"

# Grep inside compressed VCF
zgrep -v "^#" variants.vcf.gz | wc -l
```

---

## 🔄 Combine with Other Tools

```bash
# Get gene lines and show only column 3 (feature type)
grep "gene" annotation.gff | cut -f3

# Count number of lines matching a pattern
grep "BRCA1" genes.txt | wc -l
```

---

## ⚠️ Common Pitfalls

| Problem | Fix |
|--------|-----|
| No output found | Check for case: use `-i` |
| Matching too much | Use `^` for start, `$` for end |
| Grepping gzipped file directly | Use `zgrep` or `zcat | grep` |
| Matching partial word | Use `-w` for exact word match |

---

## ✅ Summary Table

| Task | Command |
|------|---------|
| Search for pattern | `grep "gene" file.txt` |
| Ignore case | `grep -i "gene"` |
| Exclude pattern | `grep -v "scaffold"` |
| Match regex (OR) | `grep -E "CDS|exon"` |
| Search compressed | `zgrep "chr1" file.gz` |
| Count matches | `grep "X" file | wc -l` |

---

## 📘 Final Note

`grep` is your **first and fastest filter**. If you're ever working with biological text data, you’ll use `grep` daily to find what matters, filter out noise, and isolate important rows.

Master it once  and it’ll serve you for life.


