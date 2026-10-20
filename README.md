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


# Run log:
```shell
#######Run#######
N E X T F L O W  ~  version 21.04.0
========== Run_GINGER.cfg ==========
##Info
☆data_work_mode=slurm                         #local/slurm
☆data_sample_name=NIP                         #sample name
☆data_max_retries=2                           #nextflow max retries
☆data_genome_fa=00.data/genome_unmask.fa      #unmask genome
☆data_mask_genome=00.data/genome_masked.fa    #soft-masked(A->a) genome
☆data_RM_out=00.data/genome_RM2.out           #RepeatMasker output
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
images_path=00.data/zgtools_v0.1.5.sif

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
Duration    : 6h 27m 46s
CPU hours   : 616.7 (1.3% failed)

#######Results#######
Output: /project/test/NIP/output_of_GINGER-mod/

```
