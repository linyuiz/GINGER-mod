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
#######Data#######
##Info
☆data_work_mode=local                         #work mode(local|slurm)
☆data_sample_name=Fungi                       #sample name
☆data_max_retries=3                           #nextflow max retries
☆data_genome_fa=00.data/genome_unmask.fa      #unmask genome
☆data_mask_genome=00.data/genome_masked.fa    #soft-masked(A->a) genome
☆data_RM_out=none                             #RepeatMasker output(.out|none)
☆data_rnaseq_list=00.data/used.trans.list     #RNAseq list
☆data_homopep_list=00.data/used.homo.list     #homology protein list
##TransAnno
hisat_para_n=2                                 #hisat parallel task num
hisat_each_threads=30                          #hisat each task threads(multi tasks)
stringtie_threads=60                           #stringite_threads(only 1 task)
trinity_threads=60                             #trinity threads(only 1 task)
trinity_memory=100G                            #trinity max memory
gmap_threads=60                                #gmap threads(only 1 task)
##HomoAnno
spaln_para_n=3                                 #spaln parallel task num
spaln_each_threads=30                          #spaln threads(multi tasks)
##DenovoAnno
augustus_train_threads=60                      #augustus train threads(only 1 task)
augustus_predict_threads=60                    #augustus predict threads
##Images
images_bind="-B /project"
images_path=/project501/zhangyaolong/Docker/02.github_images/zgtools

#######Run#######
N E X T F L O W  ~  version 21.04.0
Launching `/pipeline/zgtools/scripts/nextflow/ginger/ginger-mod.nf` [berserk_banach] - revision: 23b1dabf34
temp dir   = /project/fungi/tmp_of_GINGER-mod
output dir = /project/fungi/output_of_GINGER-mod
executor >  local (15)
[8a/9aea4f] process > hisat_index (Fungi)        [100%] 1 of 1 ✔
[95/4fa8d6] process > hisat_align (5-1)          [100%] 2 of 2 ✔
[d0/b0f09b] process > bam_merge (Fungi)          [100%] 1 of 1 ✔
[35/13fe72] process > stringtie (Fungi)          [100%] 1 of 1 ✔
[be/cfdd46] process > trans_orf (Fungi)          [100%] 1 of 1 ✔
[c7/21d3de] process > learn_1st (Fungi)          [100%] 1 of 1 ✔
[2b/012b08] process > learn_2nd (Fungi)          [100%] 1 of 1 ✔
[fe/0c96d1] process > trinity (Fungi)            [100%] 1 of 1 ✔
[a0/7c20e7] process > trans_align (Fungi)        [100%] 1 of 1 ✔
[07/935ba1] process > spaln (Morchella_brunnea)  [100%] 3 of 3 ✔
[cd/5c488c] process > homology_filter (Fungi)    [100%] 1 of 1 ✔
[a9/66127f] process > augustus_train (Fungi)     [100%] 1 of 1 ✔
[9d/5a3f40] process > augustus_prepare (Fungi)   [100%] 1 of 1 ✔
[ed/e787cd] process > augustus_predict (Fungi)   [100%] 1 of 1 ✔
[42/7bb8dd] process > snap (learn_2nd)           [100%] 1 of 1 ✔
[a2/ce4558] process > prepare_evidence (Fungi)   [100%] 1 of 1 ✔
[7c/01ed28] process > reconstruct (Fungi)        [100%] 1 of 1 ✔
[04/a45ad3] process > finalize_genes (Fungi)     [100%] 1 of 1 ✔
Duration    : 4h 6m 17s
CPU hours   : 330.1 
Succeeded   : 24

#######Results#######
Output: /project/fungi/output_of_GINGER-mod/
```
