# 🔁 Redirection and Pipes in Linux for Bioinformatics

## 🧾 What Is This?

This guide is your beginner-friendly introduction to **redirection (`>`, `>>`, `<`)** and **pipes (`|`)** in Linux, specifically tailored for bioinformatics users. These tools help you save output, chain commands, and build custom workflows — all without needing to open files manually.

Once you understand redirection and pipes, you can easily build your own one-liner pipelines and automate entire analyses using tools like `bwa`, `samtools`, `fastqc`, `awk`, `grep`, and even workflow managers like Snakemake or Nextflow.

---

## 🎯 Who Is This For?

| You are... | Is this for you? |
|------------|------------------|
| New to Linux and command-line tools | ✅ Yes |
| Running tools like FastQC, BWA, or SAMtools | ✅ Absolutely |
| Tired of creating intermediate files | ✅ Definitely |
| Still copying results into Excel 😬 | ❗You *really* need this guide |

---

## 📤 Redirecting Output

Redirection allows you to **save the output of a command into a file**, or **read input from a file**, instead of manually copying and pasting.

| Operator | Function |
|----------|----------|
| `>` | Save output to file (overwrite if it exists) |
| `>>` | Append output to an existing file |
| `<` | Use a file as input to a command |

### 🧪 Examples

```bash
# Save read headers from FASTQ (overwrite if file exists)
zcat sample_R1.fastq.gz | grep "^@" > headers.txt

# Append more headers from R2 file
zcat sample_R2.fastq.gz | grep "^@" >> headers.txt

# Use a list of gene names to filter a GFF file
grep -f gene_names.txt annotation.gff > matched_genes.gff
```

---

## 🔗 Piping Between Commands (`|`)

Pipes connect commands together by passing the output of one command directly as input to the next — no temporary files needed.

| Command | What It Does |
|---------|--------------|
| `zcat file.gz \| grep "chr1"` | Search inside a compressed file |
| `cat file.txt \| wc -l` | Count number of lines |
| `awk '{print $1}' file \| sort \| uniq` | Extract, sort, and deduplicate first column |

---

## 📑 Save Output While Displaying It (`tee`)

The `tee` command **displays output to your terminal AND saves it to a file at the same time**.

| Command | Description |
|---------|-------------|
| `command \| tee file.txt` | Show output and save to a file |
| `command \| tee -a file.txt` | Append output to a file and show it |

```bash
# Run FastQC and save logs while displaying
fastqc sample.fastq | tee logs/fastqc_output.log
```

---

## 🧬 Real Bioinformatics Use Cases

```bash
# Count number of reads in a FASTQ (4 lines = 1 read)
zcat sample.fastq.gz | wc -l

# Extract only read headers from FASTQ
zcat sample.fastq.gz | grep "^@" > read_ids.txt

# View reads mapped to chr1 in a BAM file
samtools view aln.bam chr1 | less

# Convert sorted SAM to BAM
samtools sort aln.sam | samtools view -Sb - > sorted.bam

# Extract only PASS variants from a VCF
grep -v "^#" variants.vcf | awk '$7=="PASS"' > filtered.vcf
```

---

## 🛠️ Advanced One-Liner Pipelines

```bash
# Extract read IDs from both FASTQ files, sort and remove duplicates
zcat sample_R1.fastq.gz sample_R2.fastq.gz \
  | grep "^@" \
  | cut -d ' ' -f1 \
  | sort \
  | uniq > all_read_ids.txt
```

```bash
# Align reads with BWA and convert to BAM on the fly
bwa mem ref.fa reads.fq | samtools view -Sb - > aln.bam
```

---

## ⚠️ Common Mistakes and Fixes

| Mistake | Why It Happens | Solution |
|--------|----------------|----------|
| Accidentally overwriting files | Using `>` instead of `>>` | Use `>>` when appending |
| Mixing up `>` and `|` | Trying to redirect compressed output incorrectly | Use `|` after `zcat` or `gunzip -c` |
| Filenames with spaces or variables | Shell misinterprets file name | Wrap variables and filenames in quotes: `"$file"` |

---

## ✅ Summary

| Goal | Use |
|------|-----|
| Save output to file (overwrite) | `>` |
| Append output to file | `>>` |
| Read input from file | `<` |
| Chain commands together | `|` |
| Show and save output | `tee` |

---

## 📘 Final Note

Redirection and piping are fundamental tools in any bioinformatics workflow. Once you understand them, you’ll write faster scripts, avoid temporary files, and make your data processing more efficient and reproducible.

Keep this page bookmarked. It’s your foundation for building serious command-line pipelines.

