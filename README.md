# example of data set build using h3agwas pipeline and kgp project dataset

## descriptif command line used
command line used to created dataset using [h3agwas pipeline](https://github.com/h3abionet/h3agwas):

```
nextflow run h3abionet/h3agwas/utils/build_example_data/main.nf --pos_allgeno utils/h3agwas_all.pos  -resume -profile slurmSingularity --list_chro 1-22,X --list_chro_pheno 1-22 --output_dir allchro --output allchro
```
 dataset, can be [download here](https://www.dropbox.com/s/k0ohmk445usn3ob/allchro.tgz?dl=0) (mdm5 : 842ff36935cd8cc1784cb3db21b9c45f) has been build followed :
* extraction of [h3abionet array](https://www.h3abionet.org/h3africa-chip) positions
* position from array extracted from [1000Genome v37, release:20130502](ftp://ftp.1000genomes.ebi.ac.uk:21/vol1/ftp/release/20130502/) and format in plink
* some sex has been changed to add error
* build a phenotype using gwas catalog 
 * 19 february 2021 from [USCS](http://hgdownload.soe.ucsc.edu/goldenPath/hg19/database/gwasCatalog.txt.gz)
 * Diabetes phenotype
 *  extraction of positions from gwas catalog of KGG
 * Effect extracted of gwas catalog and simulation of phenotype using gcta 
##descriptif folder
####utils : `
* h3agwas_all.pos` : contains list of position from h3abionet array 
####
* allchro/geno_all  
*contains genotype in plink format from 2507 individuals of KGP and positions of h3abionet
 * plink file : allchro.bed  allchro.bim  allchro.fam
 * `allchro_sexsex_change_plk.ind` : list of individuals where sex has been changed to create sex error
* allchro/gwascat  
 * contains information relative to gwas catalog used to build dataset
* allchro/simul_pheno
 * folder contains information relative to phenotype simulated :
 * allchro/simul_pheno/datai/ : plink phenotype extracted from KGP corresponding at positions used to simulated phenotype
 * `allchro/simul_pheno/qual_pheno/allchro_ql.pheno` : binary phenotype 
 * `allchro/simul_pheno/quant_pheno/allchro_qt.pheno` : quantitatif phenotype
 * `allchro/simul_pheno/pheno_format/` : information relative to positions to simulated phenotype
## run h3agwas/qc on simulated data
```
nextflow -c utils/params_1000G_h3abionet.params run h3abionet/h3agwas/qc/main.nf -profile slurmSingularity -resume
```
