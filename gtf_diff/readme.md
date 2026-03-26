在构建单细胞转录组参考基因组时，默认仅保留 GTF 文件中 gene_biotype 属于以下类别的基因：
```
protein_coding
lncRNA
antisense
V(D)J 相关基因
```

这一策略来源于[Cellranger](https://www.10xgenomics.com/support/software/cell-ranger/latest/analysis/inputs/cr-3p-references), 主要是为了避免假基因给基因定量带来干扰。

然而，不同版本的 Ensembl GTF 注释文件之间存在差异。已有研究（如 [Genome annotations matter: characterizing Ensembl hg38 annotations from 2014 to 2023](https://pmc.ncbi.nlm.nih.gov/articles/PMC12679773/)）表明，随着版本更新：

- 基因数量和转录本结构会发生变化
- 更重要的是，部分基因的 gene_biotype 会被重新注释

这种变化会直接影响参考基因组的构建结果，从而导致某些基因在使用不同版本的基因组时“消失”或“出现”。

例如：

- 在 Ensembl v99 中，VEGFA 的 gene_biotype 为 polymorphic_pseudogene，因此在构建参考基因组时会被过滤掉
- 而在 Ensembl v110 中，该基因被重新注释为 protein_coding，因此被保留下来并参与表达定量

Ensembl v99 与 v110 人类基因注释的gene_biotype详细变化请参见[biotype_diff_99_vs_110.tsv](./biotype_diff_99_vs_110.tsv)。