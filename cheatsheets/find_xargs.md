# 🔍 `find` + `xargs` Cheatsheet for Bioinformatics

## 🧾 What Are `find` and `xargs`?

In large bioinformatics projects, you're often dealing with hundreds of files. `find` helps you locate them by name, size, or date. `xargs` helps you apply commands **in batch** to the files `find` returns.

Together, they let you automate tasks like running FastQC on all FASTQ files, converting BAMs, or deleting junk files.

---

## 🎯 Why Bioinformaticians Use These

| Need to... | Tool | Use |
|------------|------|-----|
| Find all `.fastq.gz` files | `find` | ✅ |
| Run `fastqc` on 100s of files | `xargs` | ✅ |
| Delete temporary files | `find` + `-delete` | ✅ |
| Pipe file names into commands | `xargs` | ✅ |

---

## 📂 `find`: Locate Files

```bash
# Find all FASTQ files in current dir and subdirs
find . -name "*.fastq.gz"

# Find all BAMs in /data that are >1GB
find /data -name "*.bam" -size +1G

# Find empty files
find . -type f -empty

# Find files modified in last 7 days
find . -name "*.fq.gz" -mtime -7
```

---

## 🧰 `xargs`: Apply Commands to Files

```bash
# Run FastQC on each .fastq.gz file
find . -name "*.fastq.gz" | xargs fastqc

# Compress all .txt files
find . -name "*.txt" | xargs gzip

# Count reads in all .fastq.gz files
find . -name "*.fastq.gz" | xargs -I{} zcat {} | grep "^@" | wc -l
```

---

## 📦 Combined Use: Examples

```bash
# Run BWA on all FASTQ files
find ./reads -name "*.fastq.gz" \
  | xargs -I{} bwa mem ref.fa {} > aln.sam

# Delete all SAM files (use with caution!)
find . -name "*.sam" -delete

# Change permissions for all scripts
find . -name "*.sh" | xargs chmod +x
```

---

## 💬 What Does `-I{}` Mean?

It tells `xargs` to replace `{}` with each file name from `find`.

```bash
# Echo each file name one by one
find . -name "*.bam" | xargs -I{} echo "Processing {}"
```

---

## 🔄 Loop Alternative (for clarity)

Sometimes a `for` loop is easier to understand:

```bash
# Loop through files and run FastQC
for file in *.fastq.gz; do
  fastqc "$file"
done
```

But `find | xargs` is faster and safer in big pipelines.

---

## ⚠️ Common Pitfalls

| Problem | Why It Happens | Solution |
|--------|----------------|----------|
| Spaces in filenames | Breaks `xargs` | Use `find -print0 | xargs -0` |
| Files deleted unintentionally | `find -delete` is powerful | ALWAYS test with `-print` first |
| Argument list too long | Too many files | Use `xargs` instead of `*` |
| Too complex for simple tasks | Use `for file in *.bam` | Simpler and readable |

---

## ✅ Summary Table

| Task | Command |
|------|---------|
| Find FASTQ files | `find . -name "*.fastq.gz"` |
| Run FastQC on all | `find . -name "*.fastq.gz" \| xargs fastqc` |
| Delete `.sam` files | `find . -name "*.sam" -delete` |
| Count reads | `find . -name "*.fastq.gz" \| xargs -I{} zcat {} \| grep "^@" \| wc -l` |

---

## 📘 Final Note

Once you understand `find` and `xargs`, you can scale your analyses to hundreds of files  without renaming or scripting every step. You’ll automate 90% of your repetitive work and avoid wasting time on file-by-file operations.

This is where bioinformatics turns into real productivity.


