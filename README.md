# Elective-Module
Commands used during the project.
## Does radiation cause TE activity:
### DNApipeTE
#### Mount your working directories onto the docker container
```
 docker run -it -v /NVME2/Scratch/merrbii/chernobylData/rawReads:/mnt/input_raw_reads -v /NVME2/Scratch/merrbii/chernobylData/repAnnotations/TE_libraries:/mnt/te_library -v /home/bkhan/Scratch/chernobylData/dnapipite_results:/mnt/output clemgoub/dnapipete:latest
```
Once you are inside the container, run dnapipete on your reads.
#### Run DNApipeTE
```
 python3 dnaPipeTE.py -input /mnt/input_raw_reads/SRR24686392_1.fastq.gz   -output /mnt/output/mauritius/1iteration/ -RM_lib /mnt/te_library/Otip_combined.deNovo-repeats.Dfam3.7.Nematodes_curatedonly.fa -genome_size 60424282 -genome_coverage 0.1 -sample_number 1 -cpu 30
```
