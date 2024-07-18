# Elective-Module
Commands used during the project.
## Does radiation cause TE activity:
### DNApipeTE:
Used to quantify TEs in a sample.
#### Mount your working directories onto the dDNApipeTE docker container:
```
 docker run -it -v /NVME2/Scratch/merrbii/chernobylData/rawReads:/mnt/input_raw_reads -v /NVME2/Scratch/merrbii/chernobylData/repAnnotations/TE_libraries:/mnt/te_library -v /home/bkhan/Scratch/chernobylData/dnapipite_results:/mnt/output clemgoub/dnapipete:latest
```
Once inside the container, run dnapipete on your reads.
#### Run DNApipeTE:
```
 python3 dnaPipeTE.py -input /mnt/input_raw_reads/SRR24686392_1.fastq.gz   -output /mnt/output/mauritius/1iteration/ -RM_lib /mnt/te_library/Otip_combined.deNovo-repeats.Dfam3.7.Nematodes_curatedonly.fa -genome_size 60424282 -genome_coverage 0.1 -sample_number 1 -cpu 30
```
Run dnapipete one by one on your reads both the controls and the treatments.
### Extract some of the reads from the samples and make a pooled data using seqkit:
Randomly extract 10% of the reads from all the samples and make pooled data one for the controls and one for the treatments and later run dnapipete on this data.
#### Controls:
DF5062.Philipines.SRR24686397:
```
seqkit sample -p 0.1 -s 3000 DF5062.Philipines.SRR24686397_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_controls/subsampled.DF5062.Philipines.SRR24686397_1.fastq.gz
```
DF5123.Mauritius.SRR24686392:
```
seqkit sample -p 0.1 -s 875649 DF5123.Mauritius.SRR24686392_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_controls/subsampled.DF5123.Mauritius.SRR24686392_1.fastq.gz
```
DF5111.Australia.SRR24686394:
```
 seqkit sample -p 0.1 -s 19876 DF5111.Australia.SRR24686394_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_controls/subsampled.DF5111.Australia.SRR24686394_1.fastq.gz
```
DF5110.USA.SRR24686395:
```
 seqkit sample -p 0.1 -s 9999 DF5110.USA.SRR24686395_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_controls/subsampled.DF5110.USA.SRR24686395_1.fastq.gz
```
DF5103.Germany.SRR24686396:
```
 seqkit sample -p 0.1 -s 254000 DF5103.Germany.SRR24686396_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_controls/subsampled.DF5103.Germany.SRR24686396_1.fastq.gz
```
Concatenate your files into one file.
cat *fastq.gz > concatenated_pooled_data_controls.fastq

Now mount your working directories accordingly and run dnapipete.
```
 python3 dnaPipeTE.py -input /mnt/input_reads/concatenated_pooled_data_controls.fastq -output /mnt/output/2iteration/ -RM_lib /mnt/te_library/Otip_combined.deNovo-repeats.Dfam3.7.Nematodes_curatedonly.fa -genome_size 60424282 -genome_coverage 0.1 -sample_number 2 -cpu 30
```
N50 was highest at iteration 2 (N50 -> 5802)

#### Treatments:
QG3598.CEZ.SRR24686413:
```
seqkit sample -p 0.1 -s 5798 QG3598.CEZ.SRR24686413_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3598.CEZ.SRR24686413_1.fastq.gz
```
QG3580.CEZ.SRR24686412:
```
seqkit sample -p 0.1 -s 67798 QG3580.CEZ.SRR24686412_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3580.CEZ.SRR24686412_1.fastq.gz
```
QG3609.CEZ.SRR24686411:
```
seqkit sample -p 0.1 -s 7 QG3609.CEZ.SRR24686411_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3609.CEZ.SRR24686411_1.fastq.gz
```
QG3587.CEZ.SRR24686410:
```
seqkit sample -p 0.1 -s 567 QG3587.CEZ.SRR24686410_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3587.CEZ.SRR24686410_1.fastq.gz
```
QG3571.CEZ.SRR24686409:
```
seqkit sample -p 0.1 -s 4258947 QG3571.CEZ.SRR24686409_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3571.CEZ.SRR24686409_1.fastq.gz
```
QG3551.CEZ.SRR24686408:
```
 seqkit sample -p 0.1 -s 175647 QG3551.CEZ.SRR24686408_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3551.CEZ.SRR24686408_1.fastq.gz
```
QG3619.CEZ.SRR24686407:
```
 seqkit sample -p 0.1 -s 9875647 QG3619.CEZ.SRR24686407_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3619.CEZ.SRR24686407_1.fastq.gz
```
QG3553.CEZ.SRR24686406:
```
seqkit sample -p 0.1 -s 8760985 QG3553.CEZ.SRR24686406_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3553.CEZ.SRR24686406_1.fastq.gz
```
QG3554.CEZ.SRR24686405:
```
seqkit sample -p 0.1 -s 354697 QG3554.CEZ.SRR24686405_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3554.CEZ.SRR24686405_1.fastq.gz
```
QG3560.CEZ.SRR24686403:
```
seqkit sample -p 0.1 -s 15000 QG3560.CEZ.SRR24686403_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3560.CEZ.SRR24686403_1.fastq.gz
```
QG3559.CEZ.SRR24686402:
```
seqkit sample -p 0.1 -s 7500 QG3559.CEZ.SRR24686402_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3559.CEZ.SRR24686402_1.fastq.gz
```
QG3897.CEZ.SRR24686401:
```
seqkit sample -p 0.1 -s 2500 QG3897.CEZ.SRR24686401_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3897.CEZ.SRR24686401_1.fastq.gz
```
QG3753.CEZ.SRR24686400:
```
seqkit sample -p 0.1 -s 3000  QG3753.CEZ.SRR24686400_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3753.CEZ.SRR24686400_1.fastq.gz
```
QG3894.CEZ.SRR24686398:
```
seqkit sample -p 0.1 -s 3000  QG3894.CEZ.SRR24686398_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3894.CEZ.SRR24686398_1.fastq.gz
```
QG3912.CEZ.SRR24686399:
```
seqkit sample -p 0.1 -s 3000 QG3912.CEZ.SRR24686399_1.fastq.gz > /home/bkhan/Scratch/chernobylData/dnapipite_results/pooled_data_treatments/subsampled.QG3912.CEZ.SRR24686399_1.fastq.gz
```
Concatenate your files into one file.
cat *fastq.gz > concatenated_pooled_data_CEZ.fastq 
Run dnapipete:
```
python3 dnaPipeTE.py -input /mnt/input_reads/concatenated_pooled_data_CEZ.fastq -output /mnt/output/2iteration/ -RM_lib /mnt/te_library/Otip_combined.deNovo-repeats.Dfam3.7.Nematodes_curatedonly.fa -genome_size 60424282 -genome_coverage 0.1 -sample_number 2 -cpu 30
```
N50 was highest at iteration 2 (N50  -> 6313)

### Detettore:
#### Index the reference genome.
```
 bwa index -p ref_index CEZ-166.1.GCA_037178975.1_ASM3717897v1_genomic.fna
```
#### Check quality of the reads with fastqc:
```
fastqc *.fastq.gz
```
#### Trimm using trimmomatic:
```
 ls *_1.fastq.gz | sed 's/_1.fastq.gz//g' | nice parallel --jobs 15 --eta 'java -jar /home/bkhan/Scratch/program/Trimmomatic-0.39/trimmomatic-0.39.jar PE {}_1.fastq.gz {}_2.fastq.gz paired/{}_paired_1.fastq.gz unpaired/{}_unpaired_1.fastq.gz paired/{}_paired_2.fastq.gz unpaired/{}_unpaired_2.fastq.gz SLIDINGWINDOW:4:20 MINLEN:40'
```
#### Align and Sort reads:
```
#!/bin/bash

# Path to indexed reference genome files (without the file extension)
REF_PREFIX="/home/bkhan/Scratch/chernobylData/genome/ref_index"

# Path to paired-end reads directory
PAIRED_DIR="/home/bkhan/Scratch/chernobylData/rawReads/paired"

# Directory to save sorted BAM files
OUTPUT_DIR="/home/bkhan/Scratch/chernobylData/detettore_results"


# Loop through each paired-end read pair
for R1 in ${PAIRED_DIR}/*_1.fastq.gz; do
    # Formulate the read pair filenames
    R2=${R1/_1.fastq.gz/_2.fastq.gz}

    # Extract sample name from file path
    SAMPLE=$(basename $R1 _1.fastq.gz)

    # Perform alignment with BWA MEM using 8 threads and indexed files
    bwa mem -t 8 $REF_PREFIX $R1 $R2 > ${OUTPUT_DIR}/${SAMPLE}.aligned.sam

    # Convert SAM to BAM and sort
    samtools view -@ 8 -bS ${OUTPUT_DIR}/${SAMPLE}.aligned.sam | samtools sort -@ 8 -o ${OUTPUT_DIR}/${SAMPLE}.aligned_sorted.bam -

    # Clean up intermediate SAM file
    rm ${OUTPUT_DIR}/${SAMPLE}.aligned.sam
done
```
Save this script and run it.

#### Index the bam files:
```
find /home/bkhan/Scratch/chernobylData/detettore/ -maxdepth 1 -type f -name "*.bam" -exec samtools index {} \;
```
#### Run Detettore:
Save this script and run it.
```
#!/bin/bash

# Set input files which do not change for different samples
ref="/home/bkhan/Scratch/chernobylData/genome/CEZ-166.1.GCA_037178975.1_ASM3717897v1_genomic.fna"
annot="/home/bkhan/Scratch/chernobylData/TEannotation_file/CEZ-166.1.GCA_037178975.1_ASM3717897v1_genomic.fna.out.gff"
telib="/home/bkhan/Scratch/chernobylData/TElibrary/Otip_combined.deNovo-repeats.Dfam3.7.Nematodes_curatedonly.fa"
bampath_file="/home/bkhan/Scratch/chernobylData/detettore/paths_to_bam.txt"

# Ensure the commands file is empty or create it if it doesn't exist
> run_detettore.cmds

# Check if the BAM path file exists
if [ ! -f "$bampath_file" ]; then
  echo "Error: BAM path file $bampath_file does not exist."
  exit 1
fi

# Create a list of detettore commands, looping through a list containing paths to bam files.
while IFS= read -r bampath; do
  # Check if bampath is empty
  if [ -z "$bampath" ]; then
    echo "Warning: Found an empty line in $bampath_file. Skipping..."
    continue
  fi

  # Extract the sample name from the BAM file path (e.g., /path/to/sample1.bam -> sample1)
  sample=$(basename "$bampath" | cut -d'.' -f1)

  # Check if sample extraction was successful
  if [ -z "$sample" ]; then
    echo "Error: Could not extract sample name from $bampath. Skipping..."
    continue
  fi

  # Construct the detettore command for each BAM file
  echo "\
detettore \
  -b $bampath \
  -r $ref \
  -a $annot \
  -t $telib \
  -o $sample \
  -m tips taps \
  -c 1 \
  --require_split \
  --keep \
  --include_invariant" >> run_detettore.cmds

done < "$bampath_file"

# Ensure the commands file is not empty before running parallel
if [ ! -s run_detettore.cmds ]; then
  echo "Error: No commands were generated. Please check the BAM paths file and the script logic."
  exit 1
fi

# Use GNU parallel to run 10 commands simultaneously. Save stderr and stdout to log files.
parallel -j10 < run_detettore.cmds 2> err.log > stdout.log
```
#### Count the number of TE insertions and Deletions:
```
import os
import pandas as pd
import gzip

def count_variants(vcf_file):
    insertions = 0
    deletions = 0
    data = []

    with gzip.open(vcf_file, 'rt') if vcf_file.endswith('.gz') else open(vcf_file, 'r') as file:
        for line in file:
            if line.startswith('#'):
                continue
            columns = line.strip().split('\t')
            chrom = columns[0]
            pos = columns[1]
            ref = columns[3]
            alt = columns[4]
            info_field = columns[7]
            info_parts = info_field.split(';')

            svtype = None
            svlen = None
            end = None
            meinfo = None
            homseq = None
            homlen = None

            for part in info_parts:
                if part.startswith('SVTYPE='):
                    svtype = part.split('=')[1]
                elif part.startswith('SVLEN='):
                    svlen = part.split('=')[1]
                elif part.startswith('END='):
                    end = part.split('=')[1]
                elif part.startswith('MEINFO='):
                    meinfo = part.split('=')[1]
                elif part.startswith('HOMSEQ='):
                    homseq = part.split('=')[1]
                elif part.startswith('HOMLEN='):
                    homlen = part.split('=')[1]

            if svtype == 'INS':
                insertions += 1
            elif svtype == 'DEL':
                deletions += 1

            data.append([chrom, pos, ref, alt, svtype, svlen, end, meinfo, homseq, homlen])

    return insertions, deletions, data

input_folder = '/home/bkhan/Scratch/chernobylData/detettore'
output_folder = '/home/bkhan/Scratch/chernobylData/detettore/csvfiles'

if not os.path.exists(output_folder):
    os.makedirs(output_folder)

vcf_files = [f for f in os.listdir(input_folder) if f.endswith('.vcf') or f.endswith('.vcf.gz')]

for vcf_file in vcf_files:
    vcf_path = os.path.join(input_folder, vcf_file)
    insertions, deletions, data = count_variants(vcf_path)
    print(f'{vcf_file} - Total Insertions: {insertions}, Total Deletions: {deletions}')

    csv_file = os.path.join(output_folder, vcf_file.replace('.vcf.gz', '').replace('.vcf', '') + '_variants.csv')
    df = pd.DataFrame(data, columns=['CHROM', 'POS', 'REF', 'ALT', 'SVTYPE', 'SVLEN', 'END', 'MEINFO', 'HOMSEQ', 'HOMLEN'])
    df.to_csv(csv_file, index=False)
    print(f'Saved CSV for {vcf_file} to {csv_file}')
```
#### Create comparison plot from the csv files:
```
import os
import pandas as pd
import matplotlib.pyplot as plt

def process_csv_files(input_folder):
    csv_files = [f for f in os.listdir(input_folder) if f.endswith('.csv')]
    summary = []

    for csv_file in csv_files:
        csv_path = os.path.join(input_folder, csv_file)
        df = pd.read_csv(csv_path)

        insertions = df[df['SVTYPE'] == 'INS'].shape[0]
        deletions = df[df['SVTYPE'] == 'DEL'].shape[0]
        print(f'{csv_file} - Total Insertions: {insertions}, Total Deletions: {deletions}')

        summary.append({'File': csv_file, 'Insertions': insertions, 'Deletions': deletions})

    return summary

def plot_summary(summary, output_folder):
    if not os.path.exists(output_folder):
        os.makedirs(output_folder)

    df_summary = pd.DataFrame(summary)
    df_summary.plot(kind='bar', x='File', y=['Insertions', 'Deletions'], figsize=(12, 6), color=['blue', 'red'])
    plt.xlabel('CSV Files')
    plt.ylabel('Count')
    plt.title('Insertions and Deletions across CSV Files')
    plt.xticks(rotation=45, ha='right')
    plt.tight_layout()
    plt.savefig(os.path.join(output_folder, 'comparison_plot.png'))
    plt.show()
    print(f'Comparison plot saved to {os.path.join(output_folder, "comparison_plot.png")}')

def main(input_folder, output_folder):
    summary = process_csv_files(input_folder)
    plot_summary(summary, output_folder)

if __name__ == '__main__':
    input_folder = '/home/bkhan/Scratch/chernobylData/detettore/csvfiles'
    output_folder = '/home/bkhan/Scratch/chernobylData/detettore/csvfiles/plots'
    main(input_folder, output_folder)
```



    












