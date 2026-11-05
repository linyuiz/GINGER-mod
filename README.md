# Introduction（GINGER）
⭐️[GINGER original github](https://github.com/i10labtitech/GINGER)   
`GINGER` is a tool that is implemented an integrated method for gene
structure prediction in higher eukaryotes. RNA-Seq-based methods,
ab initio-based methods, homology-based methods are performed, and then 
gene structures are reconstructed via dynamic programming with appropriately
weighted and scored exon/intron/intergenic regions. Different prediction
processes and filtering criteria are applied to multi-exon and single-exon
genes. This pipeline is implemented using `Nextflow`.    

# Introduction（GINGER-mod）
`GINGER-mod` is a modified version of `GINGER`, featuring the following enhancements:

1️⃣ Refactor the `nextflow + shell` pipeline to improve script readability and maintainability.

2️⃣ Support both `local` execution and `slurm` cluster deployment, ensuring seamless job scheduling and resource management across environments.

3️⃣ The current output will provide a UTR-containing GFF file along with more detailed GFF statistical results.

4️⃣ Added comparison of elements such as gene/CDS/intron/exon between individual evidence GFFs and the final GFF.

5️⃣ Provide enhanced resumption capabilities for convenient continuation of interrupted runs, minimizing redundant computation and facilitating incremental updates.

6️⃣ Fixed some software bugs and adjusted the parallelization strategy.

⭐️If you encounter any issues, feel free to ask in the issue section. Please also support the original authors. **If you use `GINGER-mod`, kindly cite it:**   
Taniguchi T, Okuno M, Shinoda T, Kobayashi F, Takahashi K, Yuasa H, Nakamura Y, Tanaka H, Kajitani R, Itoh T. GINGER: an integrated method for high-accuracy prediction of gene structure in higher eukaryotes at the gene and exon level. DNA Res. 2023 Aug 1;30(4) <https://doi.org/10.1093/dnares/dsad017>

---

# Other modified versions of the software
⭐️ [**CPhasing-mod**](https://github.com/linyuiz/CPhasing-mod): Revised version of the genome scaffolding software [**C-Phasing**](https://wangyibin.github.io/CPhasing/).

⭐️ [**EDTA-mod**](https://github.com/linyuiz/EDTA-mod): Revised version of the TE annotation software [**EDTA**](https://github.com/oushujun/EDTA).

⭐️ [**GINGER-mod**](https://github.com/linyuiz/GINGER-mod): Revised version of the genome annotation software [**GINGER**](https://github.com/i10labtitech/GINGER).

---

# Installation
<p align="center"><strong>[ <a href="https://github.com/linyuiz/zgtools/wiki/English">English Wiki</a> | <a href="https://github.com/linyuiz/zgtools/wiki/%E7%AE%80%E4%BD%93%E4%B8%AD%E6%96%87">中文维基</a> ]</strong></p>
