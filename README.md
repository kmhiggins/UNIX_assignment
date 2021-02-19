#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```
head -n 5 fang_et_al_genotypes.txt
wc -l fang_et_al_genotypes.txt
awk -F "\t" '{print NF;exit}' fang_et_al_genotypes.txt
file fang_et_al_genotypes.txt
```

By inspecting this file I learned that:

1. This file has 2783 lines
2. This file has 986 columns
3. The gene names are the column names
4. There is no commented out header line
5. There is no non-ASCII text 


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
here is my snippet of code used for data processing
```

Here is my brief description of what this code does


###Teosinte Data

```
here is my snippet of code used for data processing
```

Here is my brief description of what this code does
