---
---

# Structural Variant Data
Upcoming data will be included in BRAVO's region views.
Large (>50bp) insertions, deletions, inversion.

- Data processed
- UI in development

## Data Processed

- Bash script 
- Bespoke c++ tooling
- Based on [Samplot](https://github.com/ryanlayer/samplot)
- Will be translated to nextflow 

```sh

# Extract region of interest from CRAM
samtools view -x XA -b \
  --reference ${REF_FILE} ${CRAM} \
  "${CHR}:${START}-${END}" > ${PIPE_NAME} &

# Merge all crams in a single pipe
PIPE_MERGE="pipes/pipe_${REGION}_merge.bam"
mkfifo "${PIPE_MERGE}"
samtools merge -f -o "${PIPE_MERGE}" "${PIPES[@]}" &
```

# Allele Frequencies
Upcoming data to be included in BRAVO's variant views.
TopMED Ancestry Allele Frequencies. 

- Based on TopMED freeze 8 data
- Comliment to gnomAD and 1000Genomes
