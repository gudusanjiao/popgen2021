# Population Structure
Nan Hu / Feb. 25, 2021

---
## Aims:
1. Calculating Fst between males and females using 'vcftools'
2. Calculating Fst between *S. nivalis* and *S. reticulata* using 'vcftools'
3. Identifying Fst outliers
4. Calculating d<sub>XY</sub> between males and females **(Will be done by Nan)**
5. Doing structure analysis across three species **(Will be done by Nan)**
6. Plotting Fst manhattan plots, d<sub>XY</sub> plots
---
## Calculating Fst between males and females using 'vcftools'
Population structure focuses on comparisons among subpopulations with different isolation and migration histories. When inferring population structure, Fst is an estimator as the degree of measuring Wahlund effect. In our population data, we do not really have samples of subpopulations from the same species. Instead, luckily, all of our species are dioecious which having males and females. We could treat males and females as two different subpopulations and they certainly having some different patterns in selection and life history. 

We use 'vcftools' `--weir-fst-pop` tools to calculate Fst between populations. The two argument are the individual name lists for each gender.
> Name list files are under `popgen2021/doc` directory as our last exercise.
```bash
#!/bin/bash
#SBATCH -J fst_mf
#SBATCH -o %x.o%j
#SBATCH -e %x.e%j
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH -n 16

vcftools --vcf snivalis.vcf --weir-fst-pop male.list --weir-fst-pop female.list --out snivalis

```
The output will have a suffix of `.weir.fst`. It contains columns of positions and Fst estimation.

## Calculating Fst between *S. nivalis* and *S. reticulata* using 'vcftools'
As we described above, we do not have datasets for multiple subpopulations. However, since *S. nivalis* and *S. reticulata* are closed related species sharing lots of characters, we could try to estimate Fst between these two species to see any outliers denoting the differences in each population.
> You could find merged VCF as well as the namelist file under `/lustre/scratch/nhu/popgen2021/script/popstruc/`.
```bash
#!/bin/bash
#SBATCH -J fst_sn_sr
#SBATCH -o %x.o%j
#SBATCH -e %x.e%j
#SBATCH -p nocona
#SBATCH -N 1
#SBATCH -n 16

vcftools --vcf merged_sr_sn.vcf --weir-fst-pop SN.namelist --weir-fst-pop SR.namelist --out sr_sn

```

## Plotting Fst plots and find the outliers
See [R code](https://github.com/gudusanjiao/popgen2021/blob/main/Rcode/R_manhattan_plot.R) of plotting. Note that, high Fst loci mean that between two populations, these positions are highly different. For example, in our male and female Fst analysis, loci have the high Fst means the loci that have the most differences between males and females. Thus, these loci are candidates of sex linked loci. After we check the association of sex determination of these loci, we could determine the boundary of sex determination region from this result.

## Calculating d<sub>XY</sub> between males and females 
## Doing structure analysis across three species **(Will be done by Nan)**
See [R function](https://github.com/gudusanjiao/popgen2021/blob/main/Rcode/dxy_function.R) to calculte pairwise d<sub>XY</sub> using `.vcf` as input.









