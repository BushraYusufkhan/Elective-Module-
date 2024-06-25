# Elective-Module
Commands used during the project.
## Does radiation cause TE activity:
### Run DNApipeTE on your reads:
#### Mount your working directories onto the docker container:
```
 docker run -it -v /NVME2/Scratch/merrbii/chernobylData/rawReads:/mnt/input_raw_reads -v /NVME2/Scratch/merrbii/chernobylData/repAnnotations/TE_libraries:/mnt/te_library -v /home/bkhan/Scratch/chernobylData/dnapipite_results:/mnt/output clemgoub/dnapipete:latest
```
Once you are inside the container, run dnapipete on your reads.
#### Run DNApipeTE:
```
 python3 dnaPipeTE.py -input /mnt/input_raw_reads/SRR24686392_1.fastq.gz   -output /mnt/output/mauritius/1iteration/ -RM_lib /mnt/te_library/Otip_combined.deNovo-repeats.Dfam3.7.Nematodes_curatedonly.fa -genome_size 60424282 -genome_coverage 0.1 -sample_number 1 -cpu 30
```
Run dnapipete one by one on your reads both the controls and the treatments. The parameters -genome_size and -genome_coverage were the same for all the reads.
### Extract some of the reads from the samples and make a pooled data using seqkit:
Randomly extract 10% of the reads from all the samples and make pooled data one for the control and one for the treatments and later run dnapipete on this data.
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
concatenate your files into one file.
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






