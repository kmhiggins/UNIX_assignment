#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```
head -n 5 fang_et_al_genotypes.txt
wc -l fang_et_al_genotypes.txt
awk -F "\t" '{print NF;exit}' fang_et_al_genotypes.txt
file fang_et_al_genotypes.txt
sort -k1,1V -c fang_et_al_genotypes.txt
```

By inspecting this file I learned that:

1. This file has 2783 lines
2. This file has 986 columns
3. The gene names are the column names
4. There is no commented out header line
5. There is no non-ASCII text 
6. There is disorcer with SL-15 


###Attributes of `snp_position.txt`

```
head -n 5 snp_position.txt
wc -l snp_position.txt
awk -F "\t" '{print NF;exit}' snp_position.txt
file snp_position.txt
sort -k1,1V -c snp_position.txt
```

By inspecting this file I learned that:

1. There are 984 lines in this file
2. There are just 15 columns in this file
3. There is no non-ASCII text in this file
4. There is no commented out header lines
5. The gene names are in the first column
6. There is disorder in the sorting (specifically says Fea2.1)

##Data Processing

###Maize Data

```
grep -E "(Sample_ID|ZMMIL|ZMMLR|ZMMMR)" fang_et_al_genotypes.txt > maize_geno.txt
awk -f transpose.awk maize_geno.txt > transposed_maize_geno.txt
tail -n +2 snp_position.txt | sort -k1,1 > snp_position_sorted.txt
tail -n +4 transposed_maize_geno.txt | sort -k1,1 > maize_geno_sorted.txt
join -1 1 -2 1 -t $'\t' snp_position_sorted.txt maize_geno_sorted.txt > maize_comb.txt
mkdir -p Maize_Files/{Increasing_SNPs, Decreasing_SNPs}
awk -F "\t" '$3 ~ /2/' maize_comb.txt | sort -t $'\t' -k4,4n > Maize_Files/Increasing_SNPs/maize_chr2.txt #for all ten chromosomes individually
awk -F "\t" '$3 ~ /2/' maize_comb.txt | sort -t $'\t' -k4,4rn | sed 's/?/-/g' > Maize_Files/Decreasing_SNPs/maize_chr02.txt #for all ten chromosomes individually
awk -F "\t" '$3 ~ /unknown/' maize_comb.txt > Maize_Files/maize_unknown.txt
awk -F "\t" '$3 ~ /multiple/' maize_comb.txt > Maize_Files/maize_multiple.txt
```

This code finds samples with the identifier "ZMMIL, ZMMLR, ZMMMR" and pulls those out while keeping the header. It then transposes the header and row names. 
Then it removes the headers on the snp_position file and transposed maize file and sorts according to the first column. 
It joins the two files based on the first column and outputs it into maize_comb.txt, it then creates a directory with two subfolders to keep the next step tidy. 
Finally the last steps divide the file by the value found in column 3 (chromosome number, unknown or multiple), then sort based off column 4 and deposit into files in their subdirectories, with replacement and reverse sort when asked for. 



###Teosinte Data

```
grep -E "(Sample_ID|ZMPBA|ZMPIL|ZMPJA)" fang_et_al_genotypes.txt > teosinte_geno.txt
awk -f transpose.awk teosinte_geno.txt > transposed_teosinte_geno.txt
tail -n +2 snp_position.txt | sort -k1,1 > snp_position_sorted.txt
tail -n +4 transposed_teosinte_geno.txt | sort -k1,1 > teosinte_geno_sorted.txt
join -1 1 -2 1 -t $'\t' snp_position_sorted.txt teosinte_geno_sorted.txt > teosinte_comb.txt
mkdir -p Teosinte_Files/{Increasing_SNPs, Decreasing_SNPs}
awk -F "\t" '$3 ~ /1/' teosinte_comb.txt | sort -t $'\t' -k4,4rn | sed 's/?/-/g' > Teosinte_Files/Decreasing_SNPs/teosinte_chr01.txt #for all 10 chromosomes individually
awk -F "\t" '$3 ~ /1/' teosinte_comb.txt | sort -t $'\t' -k4,4n > Teosinte_Files/Increasing_SNPs/teosinte_chr01.txt #For each of the ten chromosomes individually


```

This code finds samples with the identifier "ZMPBA, ZMPIL, ZMPJA" and pulls those out while keeping the header. It then transposes the header and row names. 
Then it removes the headers on the snp_position file and transposed teosinte file and sorts according to the first column. 
It joins the two files based on the first column and outputs it into teosinte_comb.txt, it then creates a directory with two subfolders to keep the next step tidy. 
Finally the last steps divide the file by the value found in column 3 (chromosome number, unknown or multiple), then sort based off column 4 and deposit into files in their subdirectories, with replacement and reverse sort when asked for.  
