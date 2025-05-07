# Tajima's D
authored by Megan Guidry

## About Tajima's D
Tajima's D is a normalized version of observed avg. pairwise difference amoung individuals across the genome minus the expected avg. pairwise difference amoung individuals across the genome.

Negative = selection removing variation or recent population expansion; 
Positive = selection maintaining variation or a recent population contraction.

[video explanation](https://www.youtube.com/watch?v=wiyay4YMq2A)

## Setup
Activate conda environment and set up files 
```
conda create -n vk python=3.8 numpy scipy
conda activate vk
pip install VCF-kit


#set up files on github repo
cd /home/mguidry/ROD_CADO/Diversity_metrics/
mkdir Tajimas_D
nano TD_analysis.md

#set up working directory on KITT and link files
cd /home/mguidry/ROD_CADO_MG_working/
mkdir Tajimas_D
cd Tajimas_D
ln -s /home/Shared_Data/ROD_CADO/analysis/raw.vcf/filtered/SNP.TRSdp10g1.FIL.vcf.gz filtered.vcf.gz
```

## [VCF-kit `tajima`](https://vcf-kit.readthedocs.io/en/latest/tajima/ )
Bins are useful for investigating particular areas of the genome that could be regions of interest. 

Sliding windows are helpful for scanning the entire genome.
```
#calculated tajimas d in bins of 10,000 bp
vk tajima 10000 10000 filtered.vcf.gz > 10kb_bin_td_filtered_vcf.tajima 

#can also do a sliding window approach 
vk tajima 100000 1000 filtered.vcf.gz > window_td_filtered_vcf.tajima

#or a continuous sliding window approach to capture every unique bin of variants that fall within 100kb of one another
##did not explore this yet as we are just looking for broad trends right now and have lots of data 
#vk tajima 100000 --sliding filtered.vcf.gz > sliding_window_td_filtered_vcf.tajima
```


Jon's code: 
https://github.com/The-Eastern-Oyster-Genome-Project/2024_Eastern_Oyster_Population_Genomics/blob/main/Oyster_Genome_Population_Genomic_Analysis.md#tajimas-d
