# 📦 Working with Compressed Files in Bioinformatics

---

## 🧾 What is This Page?

This guide helps you work with **compressed files** on the Linux command line especially `.gz`, `.tar`, and `.zip` files commonly used in bioinformatics.

Most raw sequencing data is downloaded as compressed `.fastq.gz` or `.fasta.gz`. Efficiently handling these files is a crucial skill  for saving disk space, speeding up transfers, and piping into tools without decompressing.

This cheatsheet introduces commands like `gzip`, `gunzip`, `tar`, `zcat`, and `bgzip`  with real examples in genomics and NGS workflows.

---

## 🎯 Who Is This For?

| You are... | Is this for you? |
|------------|------------------|
| A beginner dealing with `.fastq.gz` or `.tar.gz` files | ✅ Yes |
| A student downloading genomes or SRA data | ✅ Yes |
| A bioinformatician automating QC or alignment pipelines | ✅ Definitely |
| Someone new to command-line file compression | ✅ Absolutely |

---

## 📦 Compression Basics: `gzip` and `gunzip`

| Command | Use |
|--------|-----|
| `gzip file.fastq` | Compress to `file.fastq.gz` |
| `gunzip file.fastq.gz` | Decompress to `file.fastq` |
| `gzip -k file.fasta` | Compress but **keep** the original file |
| `gunzip -c file.gz > output` | Decompress to a new file (without overwriting original) |
| `gzip -r folder/` | Recursively compress all files in a folder |

💡 Most NGS files are already `.gz` — decompress only if needed.

---

## 🔍 Viewing Compressed Files Without Extracting

| Command | Description |
|--------|-------------|
| `zcat file.fastq.gz` | View contents (like `cat`) |
| `zless file.gz` | Page through like `less` |
| `zgrep pattern file.gz` | Search inside compressed file |
| `zmore`, `zhead`, `ztail` | Variants for viewing compressed data |
| `zgrep "^@" file.fastq.gz` | Find all read headers in a FASTQ |

---

## 📂 Archive Files: `tar` and `.tar.gz`

| Command | What it Does |
|--------|----------------|
| `tar -cvzf output.tar.gz folder/` | Create compressed archive |
| `tar -xvzf file.tar.gz` | Extract files from archive |
| `tar -tzf file.tar.gz` | List contents without extracting |
| `tar -xvzf file.tar.gz -C path/` | Extract to a specific folder |
| `tar -cvf data.tar data/` | Archive without compression (just `.tar`) |

### Use Case in Bioinformatics:
- Back up a full `results/` directory into `results.tar.gz` before sharing.
- Bundle multiple samples’ `.fastq.gz` into one archive.

---

## 🚀 High-Speed Compression: `pigz` (Parallel gzip)

| Command | Description |
|--------|-------------|
| `pigz file.fastq` | Compress using all CPU cores |
| `pigz -p 4 file.fastq` | Use 4 threads |
| `unpigz file.fastq.gz` | Decompress pigz-compressed file |

💡 Much faster than `gzip` — ideal for large `.fastq` or `.bam` files.  
Install with: `sudo apt install pigz`

---

## 🧬 Genomics-specific: `bgzip` and `tabix`

| Tool | Use |
|------|-----|
| `bgzip file.vcf` | Compress `.vcf` or `.bed` for indexing |
| `tabix -p vcf file.vcf.gz` | Create index for compressed VCF |
| `tabix -h file.vcf.gz chr1:1000-5000` | Extract region by coordinates |

🔬 Used when working with `.vcf.gz`, `.bed.gz`, or `.gff.gz` that need to be indexed for random access in tools like `bcftools` or `htslib`.

---

## 📚 Real-World Examples

| Task | Command |
|------|---------|
| Decompress a FASTQ file | `gunzip sample_R1.fastq.gz` |
| Peek inside compressed FASTQ | `zcat sample_R1.fastq.gz | head` |
| Compress a new genome assembly | `gzip polished_assembly.fasta` |
| Bundle and compress results | `tar -czf results.tar.gz results/` |
| Compress a large FASTA using all cores | `pigz -p 8 reference.fasta` |
| Prepare VCF for indexing | `bgzip variants.vcf && tabix -p vcf variants.vcf.gz` |

---

## 💡 Tips and Best Practices

- Use `zcat` or `zless` to avoid decompressing huge files unnecessarily
- Use `pigz` for fast compression on multi-core systems
- Use `bgzip + tabix` for genomic formats that need random access
- Avoid decompressing raw FASTQ unless absolutely needed
- Use `.tar.gz` for archiving full projects or multiple samples

---

## ✅ Summary

| You Want To… | Use This |
|--------------|----------|
| Compress/decompress single files | `gzip`, `gunzip` |
| View compressed files safely | `zcat`, `zless`, `zgrep` |
| Archive folders and backups | `tar -czf`, `tar -xvzf` |
| Compress FAST with threads | `pigz` |
| Work with genomic `.vcf.gz` or `.bed.gz` | `bgzip`, `tabix` |

---

📘 Compression is a part of nearly every workflow in genomics.  
Mastering these tools helps you work faster, store efficiently, and collaborate better.


