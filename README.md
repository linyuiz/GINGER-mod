# Introduction（GINGER）
⭐️[GINGER original github](https://github.com/i10labtitech/GINGER)   
`GINGER` is a tool that is implemented an integrated method for gene
structure prediction in higher eukaryotes. RNA-Seq-based methods,
ab initio-based methods, homology-based methods are performed, and then 
gene structures are reconstructed via dynamic programming with appropriately
weighted and scored exon/intron/intergenic regions. Different prediction
processes and filtering criteria are applied to multi-exon and single-exon
genes. This pipeline is implemented using `Nextflow`.    

⭐️If you encounter any issues, feel free to ask in the issue section. Please also support the original authors. **If you use `GINGER-mod`, kindly cite it:**   
Taniguchi T, Okuno M, Shinoda T, Kobayashi F, Takahashi K, Yuasa H, Nakamura Y, Tanaka H, Kajitani R, Itoh T. GINGER: an integrated method for high-accuracy prediction of gene structure in higher eukaryotes at the gene and exon level. DNA Res. 2023 Aug 1;30(4) <https://doi.org/10.1093/dnares/dsad017>

# Other modified versions of the software
<div align="center"><img alt="image" src="https://github.com/user-attachments/assets/729a8e17-94a4-492a-8d01-c902303c06a1" width=30%/></div>

⭐️ For the modified version of annotation tool `EviAnn`, please visit: [EviAnn-mod](https://github.com/linyuiz/EviAnn-mod) (Not recommended for now, currently under upgrade)  

⭐️ For the modified version of TE transposon annotation tool `EDTA`, please visit: [EDTA-mod](https://github.com/linyuiz/EDTA-mod) (Beta version)  

⭐️ For the modified version of scaffolding tool `C-Phasing`, please visit: [GINGER-mod](https://github.com/linyuiz/GINGER-mod) (Beta version)   

---

# Installation
## Install with conda/mamba (Linux64) 
To install, first download the latest distribution tarball：[zgtools_latest.tar.gz](https://github.com/linyuiz/zgtools/releases) (not one of the Source code files!) from the github release page：https://github.com/linyuiz/GINGER-mod/releases/. 

```shell
#1. nextflow install
mamba create -n GINGER-mod -c conda-forge -c bioconda nextflow=21.04.0=h4a94de4_0 singularity=3.8.6=hf1ae047_0
#2. zgtools GINGER-mod install
tar -zxvf zgtools*.tar.gz && cd zgtools && chmod +x zg*
#3. add zgtools to your $PATH:
echo "export PATH=$PWD:\$PATH" >>~/.bashrc && source ~/.bashrc
zgtools GINGER-mod
```
---

# Usage

You just need to soft link zgtools to your usual bin folder such as【~/bin】, or use an absolute path such as【/project/softawre/zgtools GINGER-mod】.
```shell
Usage:

        zgtools GINGER-mod Run_GINGER.cfg

        Run_GINGER.cfg     --Run Config

Example1:

        zgtools GINGER-mod example_cfg

Example2:

        zgtools GINGER-mod Run_GINGER.cfg
```

# Example
1️⃣ First, run `zgtools GINGER-mod example_cfg` to generate a sample configuration file, then modify the parameters below according to your needs:
```
Run_GINGER.cfg:
##Info
☆data_work_mode=slurm                         #local/slurm
☆data_max_retries=3                           #nextflow max retries(0|3)
☆data_genome_fa=00.data/genome_unmask.fa      #unmask genome
☆data_mask_genome=00.data/genome_masked.fa    #soft-masked(A->a) genome
☆data_RM_out=00.data/genome_RM.out            #RepeatMasker output(.out|none)
☆data_rnaseq_list=00.data/used.trans.list     #RNAseq list
☆data_homopep_list=00.data/used.homo.list     #homology protein list
##TransAnno
hisat_para_n=5                                 #hisat parallel task num
hisat_each_threads=60                          #hisat each task threads(multi tasks)
stringtie_threads=60                           #stringite_threads(only 1 task)
trinity_threads=60                             #trinity threads(only 1 task)
trinity_memory=200G                            #trinity max memory
gmap_threads=60                                #gmap threads(only 1 task)
##HomoAnno
spaln_para_n=5                                 #spaln parallel task num
spaln_each_threads=30                          #spaln threads(multi tasks)
##DenovoAnno
augustus_train_threads=60                      #augustus train threads(only 1 task)
augustus_predict_threads=60                    #augustus predict threads
##Images
images_bind="-B /project"
images_path=~/images/zgtools_v0.1.6.sif
```
2️⃣ Edit `example.used.trans.list`; currently, only second-generation transcriptomes are supported, and full-length transcriptomes are not supported.    
```
fastq   5-1     /your/absolute/path/5-1_raw_1.fq.gz,/your/absolute/path/5-1_raw_2.fq.gz
fastq   6-1     /your/absolute/path/6-1_raw_1.fq.gz,/your/absolute/path/6-1_raw_2.fq.gz
```
3️⃣ Edit `example.used.homo.list`; you can include any number of protein files from closely related species, but generally it is recommended to include 5-6 high-quality annotations.    
```
Pezizomy        Morchella_angusticeps   /your/absolute/path/Morchella_angusticeps.pep.fa
Pezizomy        Morchella_brunnea       /your/absolute/path/Morchella_brunnea.pep.fa
Pezizomy        Morchella_eximia        /your/absolute/path/Morchella_eximia.pep.fa
```
Translate the following text:
Note: The first column is mandatory for Spaln. Only modify it after checking example.splan.check.txt:    
```
Angiosp   被子植物（拟南芥、水稻、玉米等）             
Magnolio  单子叶植物（水稻、玉米、高粱、等）           
Eudicoty  双子叶植物（拟南芥、番茄、大豆等）           
Tetrapod  四足动物（人、小鼠、鸡、蛙等）               
Fish_mdl  鱼类（斑马鱼、青鳉等模式鱼）                 
InsectDm  昆虫-果蝇类（Drosophila及近缘）              
NematodC  线虫-秀丽隐杆线虫类（Caenorhabditis及近缘）  
Saccharo  酵母-酿酒酵母类（Saccharomyces及近缘）       
Schizosa  酵母-粟酒裂殖酵母类（Schizosaccharomyces）   
FungiAll  真菌通用（不挑具体类群时用）                 
ChordatC  尾索动物（海鞘、玻璃海鞘）                   
ChordatU  头索动物/无脊椎脊索动物（文昌鱼、海兔等）     
Echinode  棘皮动物（海胆、海星）                       
Mollusca  软体动物（牡蛎、鲍鱼等）                     
InsectAc  昆虫-膜翅目（蚂蚁、蜜蜂）                    
InsectAg  昆虫-蚜虫/蝽类（蚜虫、蝽）                   
InsectBm  昆虫-鳞翅目（家蚕）                          
Aconoida  顶复门（弓形虫、疟原虫，无锥体）             
Archamoe  古虫/变形虫（阿米巴、利什曼原虫）            
Conoidas  顶复门-锥体虫                                
```
example.splan.check.txt
2️⃣ Then, run `zgtools GINGER-mod Run_GINGER.cfg`. If want to stop the job, please press `Ctrl + C`, not​ `Ctrl + Z`.      

---

# Run log:
This example was tested using the rice T2T-NIP genome. You can download the genome and transcriptome data here:    
https://ngdc.cncb.ac.cn/gwh/ncbi_assembly/2417393/show   
https://ngdc.cncb.ac.cn/gsa/browse/insdc/SRA1669491/SRX20950525   
```shell
#######Run#######
N E X T F L O W  ~  version 21.04.0
========== Run_GINGER.cfg ==========
##Info
☆data_work_mode=slurm                         #local/slurm
☆data_sample_name=NIP                         #sample name
☆data_max_retries=2                           #nextflow max retries
☆data_genome_fa=00.data/genome_unmask.fa      #unmask genome(must)
☆data_mask_genome=00.data/genome_masked.fa    #soft-masked(A->a) genome(must)
☆data_RM_out=00.data/genome_RM.out            #RepeatMasker output(.out|none)
☆data_rnaseq_list=00.data/used.trans.list     #RNAseq list
☆data_homopep_list=00.data/used.homo.list     #homology protein list
##TransAnno
hisat_para_n=3                                 #hisat parallel task num
hisat_each_threads=30                          #hisat each task threads(multi tasks)
stringtie_threads=30                           #stringite_threads(only 1 task)
trinity_threads=60                             #trinity threads(only 1 task)
trinity_memory=200G                            #trinity max memory
gmap_threads=60                                #gmap threads(only 1 task)
##HomoAnno
spaln_para_n=3                                 #spaln parallel task num
spaln_each_threads=30                          #spaln threads(multi tasks)
##DenovoAnno
augustus_train_threads=60                      #augustus train threads(only 1 task)
augustus_predict_threads=60                    #augustus predict threads
##Images
images_bind="-B /project"
images_path=00.data/zgtools_v0.1.6.sif

====================================
temp dir   = /project/test/NIP/tmp_of_GINGER-mod
output dir = /project/test/NIP/output_of_GINGER-mod
[d2/d7dbc3] process > hisat_index (NIP)      [100%] 1 of 1 ✔
[f3/76e731] process > hisat_align (NIP-rna)  [100%] 1 of 1 ✔
[2b/3601fd] process > bam_merge (NIP)        [100%] 1 of 1 ✔
[10/88af2a] process > stringtie (NIP)        [100%] 1 of 1 ✔
[1a/e47953] process > trans_orf (NIP)        [100%] 1 of 1 ✔
[68/e3c852] process > learn_1st (NIP)        [100%] 1 of 1 ✔
[f4/c0ae99] process > learn_2nd (NIP)        [100%] 1 of 1 ✔
[e3/3be0db] process > trinity (NIP)          [100%] 1 of 1 ✔
[ba/949e7a] process > trans_align (NIP)      [100%] 1 of 1 ✔
[72/2fc7f3] process > spaln (ZS97RS3)        [100%] 4 of 4 ✔
[58/90445c] process > homology_filter (NIP)  [100%] 1 of 1 ✔
[fe/9f6ae9] process > augustus_train (NIP)   [100%] 1 of 1 ✔
[ab/b3cfa4] process > augustus_prepare (NIP) [100%] 1 of 1 ✔
[fc/00b3dd] process > augustus_predict (NIP) [100%] 1 of 1 ✔
[16/e05cf9] process > snap (learn_2nd)       [100%] 1 of 1 ✔
[e7/9c7b72] process > prepare_evidence (NIP) [100%] 1 of 1 ✔
[6c/998f08] process > reconstruct (NIP)      [100%] 1 of 1 ✔
[01/75536c] process > finalize_genes (NIP)   [100%] 1 of 1 ✔
[1f/74a4c7] process > gff_distribution (NIP) [100%] 1 of 1 ✔
Duration    : 6h 27m 46s
CPU hours   : 616.7 

Transcriptome Alignment Rate:
ID          MapRate(%)
NIP-rna     94.73%

Final GINGER-mod Predicted Results:
Item                                     Number
the total number of gene                 34,058
the total gene length (bp)               89,709,567
the average of gene length (bp)          2,634.02
the average cds length of per gene (bp)  1,289.33
the average exon number of per gene      4.40
the average of exon length (bp)          292.89
the average of intron length (bp)        395.25
the total number of exon                 149,927
the total number of intron               115,869
the total exon length (bp)               43,912,149
the total intron length (bp)             45,797,418

Notice:
If you have any questions, you can ask in the issue section at: https://github.com/linyuiz/GINGER-mod

#######Results#######
Output: /project/test/NIP/output_of_GINGER-mod/
.
├── GINGER.gene.cds.fa               CDS fasta
├── GINGER.gene.pep.fa               protein fasta
├── GINGER.gene.UTRs.gff             longest gff3(have UTRs)
├── GINGER.gene.UTRs.gtf             longest gtf(have UTRs)
├── GINGER.gene.gff                  longest gff3(none UTRs)
├── GINGER.gene.gtf                  longest gtf(none UTRs)
├── GINGER.gene.stat.*               longest gff3 statistics
├── GINGER.gene.gff_distribution.*   longest gff3 distribution
└── GINGER.trans.map_stat.xls        transcriptome mapping rate
```
⭐️Below is a comparison of the annotation results of the GINGER-mod version with those of other rice genome versions：
<img alt="image" src="https://github.com/user-attachments/assets/a75fa3b7-3e71-4eb9-b65f-6b045fed7fe0" width=50%/>
