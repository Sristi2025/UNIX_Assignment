#UNIX Assignment

##Data Inspection

###Attributes of `fang_et_al_genotypes`

```
here is my snippet of code used for data inspection

1. $ ls -lh fang_et_al_genotypes.txt 
2. $ wc fang_et_al_genotypes.txt 
3. $ file fang_et_al_genotypes.txt 
4. $ awk -F "\t" '{print NF; exit}' fang_et_al_genotypes.txt 

By inspecting this file I learned that:

1. Lists out the directory, size -11 megabytes, modification times and users: -rw-r--r--. 1 sristid domain users 11M Jan 29 13:44 fang_et_al_genotypes.txt
2. fang_et_al_genotypes.txt 2783 2744038 11051939 number of lines - rows
3. fang_et_al_genotypes.txt contains ASCII text, with very long lines
4. fang_et_al_genotypes.txt has 986 columns 


###Attributes of `snp_position.txt`

```
here is my snippet of code used for data inspection
1. $ ls -lh snp_position.txt 
2. $ file snp_position.txt 
3. $ wc snp_position.txt 
4. $ awk -F "\t" '{print NF; exit}' snp_position.txt 

By inspecting this file I learned that:

1. Lists out the directory, size - 81 kilobytes, modification time and users: sristid domain users 81K Jan 29 13:44 snp_position.txt
2. snp_position.txt file contains ASCII text
3. snp_position.txt file contains = 984 13198 82763 number of lines - rows
4. snp_position.txt file contains 15 number of columns


##Data Processing

###Maize Data

```
here is my snippet of code used for data processing

1. mkdir sdunixtrial1
2. cp snp_position.txt transposed_genotypes.txt sdunixtrial1
3. vim snp_position.txt; set nowrap 
4. tail -n +3 transposed_genotypes.txt> transposed_headers.txt 
5. wc transposed_headers.txt   =984 2738472 10966346 transposed_headers.txt
6. tail -n +6 transposed_headers.txt | awk -F "\t" '{print NF; exit}'   =2783 
7. sed 's/Group/SNP_ID/g' transposed_headers.txt > nogroup.txt 
8. wc nogroup.txt   =984 2738472 10966347 nogroup.txt
9. join -1 1 -2 1 -t $'\t' snp_position.txt nogroup.txt > transposed_joined.txt
10. vim transposed_joined.txt; set nowrap
11. wc transposed_joined.txt   =984 2750686 11038279 transposed_joined.txt
12. tail -n +6 transposed_joined.txt | awk -F "\t" '{print NF; exit}'   =2797
13. awk '{for(i=1;i<=NF;i++) if ($i == "ZMMIL") print "Found at column " i}' transposed_joined.txt   =Starts from 2508 and ends at 2797
14. awk '{for(i=1;i<=NF;i++) if ($i == "ZMMLR") print "Found at column " i}' transposed_joined.txt   =Starts from 1225 and ends at 2480
15. awk '{for(i=1;i<=NF;i++) if ($i == "ZMMMR") print "Found at column " i}' transposed_joined.txt   =Starts from 2481 and ends at 2507
16. awk '{for(i=1;i<=NF;i++) if ($i == "ZMMIL") count++} END{print count}' transposed_joined.txt   =290
17. awk '{for(i=1;i<=NF;i++) if ($i == "ZMMLR") count++} END{print count}' transposed_joined.txt   =1256
18. awk '{for(i=1;i<=NF;i++) if ($i == "ZMMMR") count++} END{print count}' transposed_joined.txt   =27
19. cut -d $'\t' -f1,3,4,2508-2797,1225-2480,2481-2507 transposed_joined.txt > maize.txt
20. wc maize.txt   =984 1550778 6216783 maize.txt
21. tail -n +6 maize.txt | awk -F "\t" '{print NF; exit}'   =1576
22. sort -k3,3n maize.txt > maize_sort.txt 
23. wc maize_sort.txt   =984 1550778 6216783 maize_sort.txt
24. tail -n +6 maize_sort.txt | awk -F "\t" '{print NF; exit}'   =1576
25. (head -n 1 maize.txt && tail -n +2 maize.txt | sort -k3,3n) > Maize_headersorted.txt 
26. wc Maize_headersorted.txt   =984 1550778 6216783 Maize_headersorted.txt
27. tail -n +6 Maize_headersorted.txt | awk -F "\t" '{print NF; exit}'   =1576
28. grep -v "^#" Maize_headersorted.txt | cut -f2 | sort | uniq -c 
    155 1
     53 10
    127 2
    107 3
     91 4
    122 5
     76 6
     97 7
     62 8
     60 9
      1 Chromosome
      6 multiple
     27 unknown
29. { head -n 1 Maize_headersorted.txt && awk '$2 == 1' Maize_headersorted.txt; } > Maize_chr1.txt
30. { head -n 1 Maize_headersorted.txt && awk '$2 == 2' Maize_headersorted.txt; } > Maize_chr2.txt
31. { head -n 1 Maize_headersorted.txt && awk '$2 == 3' Maize_headersorted.txt; } > Maize_chr3.txt
32. { head -n 1 Maize_headersorted.txt && awk '$2 == 4' Maize_headersorted.txt; } > Maize_chr4.txt
33. { head -n 1 Maize_headersorted.txt && awk '$2 == 5' Maize_headersorted.txt; } > Maize_chr5.txt
34. { head -n 1 Maize_headersorted.txt && awk '$2 == 6' Maize_headersorted.txt; } > Maize_chr6.txt
35. { head -n 1 Maize_headersorted.txt && awk '$2 == 7' Maize_headersorted.txt; } > Maize_chr7.txt
36. { head -n 1 Maize_headersorted.txt && awk '$2 == 8' Maize_headersorted.txt; } > Maize_chr8.txt
37. { head -n 1 Maize_headersorted.txt && awk '$2 == 9' Maize_headersorted.txt; } > Maize_chr9.txt
38. { head -n 1 Maize_headersorted.txt && awk '$2 == 10' Maize_headersorted.txt; } > Maize_chr10.txt
39. { head -n 1 Maize_headersorted.txt && awk '$2 == "multiple"' Maize_headersorted.txt; } > Maize_chrm.txt
40. { head -n 1 Maize_headersorted.txt && awk '$2 == "unknown"' Maize_headersorted.txt; } > Maize_chru.txt
41. wc Maize_chr1.txt Maize_chr2.txt Maize_chr3.txt Maize_chr4.txt Maize_chr5.txt Maize_chr6.txt Maize_chr7.txt Maize_chr8.txt Maize_chr9.txt Maize_chr10.txt Maize_chrm.txt Maize_chru.txt
    156  245856  988210 Maize_chr1.txt
    128  201728  811380 Maize_chr2.txt
    108  170208  685104 Maize_chr3.txt
     92  144992  584066 Maize_chr4.txt
    123  193848  779831 Maize_chr5.txt
     77  121352  489390 Maize_chr6.txt
     98  154448  622008 Maize_chr7.txt
     63   99288  400970 Maize_chr8.txt
     61   96136  388329 Maize_chr9.txt
     54   85104  344187 Maize_chr10.txt
      7   11026   47345 Maize_chrm.txt
     28   44128  180078 Maize_chru.txt
    995 1568114 6320898 total
42. awk -F "\t" '{print NF; exit}' Maize_chr1.txt Maize_chr2.txt Maize_chr3.txt Maize_chr4.txt Maize_chr5.txt Maize_chr6.txt Maize_chr7.txt Maize_chr8.txt Maize_chr9.txt Maize_chr10.txt Maize_chrm.txt Maize_chru.txt   =1576
43. sed 's/?/-/g' Maize_headersorted.txt > Maize_allhyphen.txt 
44. wc Maize_allhyphen.txt    =984 1550778 6216783 Maize_allhyphen.txt
45. awk -F "\t" '{print NF; exit}' Maize_allhyphen.txt    =1576
46. mkdir Maize_increasingorder.txt
47. mv Maize_chr1.txt Maize_chr2.txt Maize_chr3.txt Maize_chr4.txt Maize_chr5.txt Maize_chr6.txt Maize_chr7.txt Maize_chr8.txt Maize_chr9.txt Maize_chr10.txt Maize_chrm.txt Maize_chru.txt Maize_increasingorder.txt 
48. mkdir Maize_decreasingorder.txt
49. (head -n 1 Maize_allhyphen.txt && tail -n +2 Maize_allhyphen.txt | sort -k3,3nr) > Maize_decreasingall10.txt 
50. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 1' Maize_decreasingall10.txt; } > Md_chr1.txt
51. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 2' Maize_decreasingall10.txt; } > Md_chr2.txt
52. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 3' Maize_decreasingall10.txt; } > Md_chr3.txt
53. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 4' Maize_decreasingall10.txt; } > Md_chr4.txt
54. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 5' Maize_decreasingall10.txt; } > Md_chr5.txt
55. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 6' Maize_decreasingall10.txt; } > Md_chr6.txt
56. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 7' Maize_decreasingall10.txt; } > Md_chr7.txt
57. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 8' Maize_decreasingall10.txt; } > Md_chr8.txt
58. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 9' Maize_decreasingall10.txt; } > Md_chr9.txt
59. { head -n 1 Maize_decreasingall10.txt && awk '$2 == 10' Maize_decreasingall10.txt; } > Md_chr10.txt
60. wc Md_chr1.txt Md_chr2.txt Md_chr3.txt Md_chr4.txt Md_chr5.txt Md_chr6.txt Md_chr7.txt Md_chr8.txt Md_chr9.txt Md_chr10.txt
    156  245856  988210 Md_chr1.txt
    128  201728  811380 Md_chr2.txt
    108  170208  685104 Md_chr3.txt
     92  144992  584066 Md_chr4.txt
    123  193848  779831 Md_chr5.txt
     77  121352  489390 Md_chr6.txt
     98  154448  622008 Md_chr7.txt
     63   99288  400970 Md_chr8.txt
     61   96136  388329 Md_chr9.txt
     54   85104  344187 Md_chr10.txt
    960 1512960 6093475 total
61. awk -F "\t" '{print NF; exit}' Md_chr1.txt Md_chr2.txt Md_chr3.txt Md_chr4.txt Md_chr5.txt Md_chr6.txt Md_chr7.txt Md_chr8.txt Md_chr9.txt Md_chr10.txt   =1576



Here is my brief description of what this code does

'mkdir' created a directory to carry out the experiment further; 
changed the column ID to SNP_ID from group using 'sed' stream editor command
join -1 1 -2 1 -t  = this command helped join the files
ran the 'awk' command with 'for' and 'i' loop to find ZMMIL, ZMMMR, ZMMIR, in the joined file
using the 'cut' command, all the words in the joined file that are ZMMIL, ZMMMR, ZMMIR were cut and transfered to a new file to do further data processing
'sort -k3,3n maize.txt > maize_sort.txt'  command was used to sort the header according the given position of SNP_ID, Chromosome and position
'grep' command was used to count the number of chromosomes and the number of times each chromosome appeared
'head -n 1' and 'awk' command was used to count 10 files (1 for each chromosome) with SNPs ordered based on increasing position values and separate each chromosomes in their respective files
'sed' stream editor command was used again to change the ? symbol to - hyphen, and separate them in a new file
(head -n 1 Maize_allhyphen.txt && tail -n +2 Maize_allhyphen.txt | sort -k3,3nr) > Maize_decreasingall10.txt  - this code was used to sort the maize files in decreasing order
'head -n 1' and 'awk' command was used to count 10 files (1 for each chromosome) with SNPs ordered based on decreasing position values and separate each chromosomes in their respective files




###Teosinte Data

```
here is my snippet of code used for data processing

1. awk '{for(i=1;i<=NF;i++) if ($i == "ZMPBA") print "Found at column " i}' transposed_joined.txt 
2. awk '{for(i=1;i<=NF;i++) if ($i == "ZMPIL") print "Found at column " i}' transposed_joined.txt
3. awk '{for(i=1;i<=NF;i++) if ($i == "ZMPJA") print "Found at column " i}' transposed_joined.txt
4. awk '{for(i=1;i<=NF;i++) if ($i == "ZMPBA") count++} END{print count}' transposed_joined.txt   =900
5. awk '{for(i=1;i<=NF;i++) if ($i == "ZMPIL") count++} END{print count}' transposed_joined.txt   =41
6. awk '{for(i=1;i<=NF;i++) if ($i == "ZMPJA") count++} END{print count}' transposed_joined.txt   =34
7. cut -d $'\t' -f1,3,4,89-988,1178-1218,989-1022 transposed_joined.txt > teosinte.txt
8. wc teosinte.txt   =984 962346 3861859 teosinte.txt
9. tail -n +6 teosinte.txt | awk -F "\t" '{print NF; exit}'   =978
10. sort -k3,3n teosinte.txt > teosinte_sort.txt
11. (head -n 1 teosinte.txt && tail -n +2 teosinte.txt | sort -k3,3n) > Teosinte_headersorted.txt
12. grep -v "^#" Teosinte_headersorted.txt | cut -f2 | sort | uniq -c
    155 1
     53 10
    127 2
    107 3
     91 4
    122 5
     76 6
     97 7
     62 8
     60 9
      1 Chromosome
      6 multiple
     27 unknown
13. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 1' Teosinte_headersorted.txt; } > Teosinte_chr1.txt
14. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 2' Teosinte_headersorted.txt; } > Teosinte_chr2.txt
15. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 3' Teosinte_headersorted.txt; } > Teosinte_chr3.txt
16. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 4' Teosinte_headersorted.txt; } > Teosinte_chr4.txt
17. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 5' Teosinte_headersorted.txt; } > Teosinte_chr5.txt
18. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 6' Teosinte_headersorted.txt; } > Teosinte_chr6.txt
19. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 7' Teosinte_headersorted.txt; } > Teosinte_chr7.txt
20. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 8' Teosinte_headersorted.txt; } > Teosinte_chr8.txt
21. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 9' Teosinte_headersorted.txt; } > Teosinte_chr9.txt
22. { head -n 1 Teosinte_headersorted.txt && awk '$2 == 10' Teosinte_headersorted.txt; } > Teosinte_chr10.txt
23. { head -n 1 Teosinte_headersorted.txt && awk '$2 == "multiple"' Teosinte_headersorted.txt; } > Teosinte_chrm.txt
24. { head -n 1 Teosinte_headersorted.txt && awk '$2 == "unknown"' Teosinte_headersorted.txt; } > Teosinte_chru.txt
25. wc Teosinte_chr1.txt Teosinte_chr2.txt Teosinte_chr3.txt Teosinte_chr4.txt Teosinte_chr5.txt Teosinte_chr6.txt Teosinte_chr7.txt Teosinte_chr8.txt Teosinte_chr9.txt Teosinte_chr10.txt Teosinte_chrm.txt Teosinte_chru.txt 
    156  152568  613862 Teosinte_chr1.txt
    128  125184  504008 Teosinte_chr2.txt
    108  105624  425572 Teosinte_chr3.txt
     92   89976  362806 Teosinte_chr4.txt
    123  120294  484419 Teosinte_chr5.txt
     77   75306  304010 Teosinte_chr6.txt
     98   95844  386396 Teosinte_chr7.txt
     63   61614  249078 Teosinte_chr8.txt
     61   59658  241221 Teosinte_chr9.txt
     54   52812  213823 Teosinte_chr10.txt
      7    6840   29405 Teosinte_chrm.txt
     28   27384  111906 Teosinte_chru.txt
    995  973104 3926506 total
26. (head -n 1 Teosinte_allhyphen.txt && tail -n +2 Teosinte_allhyphen.txt | sort -k3,3nr) > Teosinte_decreasingall10.txt
27. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 1' Teosinte_decreasingall10.txt;} > Td_chr1.txt
28. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 2' Teosinte_decreasingall10.txt;} > Td_chr2.txt
29. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 3' Teosinte_decreasingall10.txt;} > Td_chr3.txt
30. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 4' Teosinte_decreasingall10.txt;} > Td_chr4.txt
31. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 5' Teosinte_decreasingall10.txt;} > Td_chr5.txt
32. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 6' Teosinte_decreasingall10.txt;} > Td_chr6.txt
33. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 7' Teosinte_decreasingall10.txt;} > Td_chr7.txt
34. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 8' Teosinte_decreasingall10.txt;} > Td_chr8.txt
35. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 9' Teosinte_decreasingall10.txt;} > Td_chr9.txt
36. { head -n 1 Teosinte_decreasingall10.txt && awk '$2 == 10' Teosinte_decreasingall10.txt;}> Td_chr10.txt
37. wc Td_chr1.txt Td_chr2.txt Td_chr3.txt Td_chr4.txt Td_chr5.txt Td_chr6.txt Td_chr7.txt Td_chr8.txt Td_chr9.txt Td_chr10.txt
    156  152568  613862 Td_chr1.txt
    128  125184  504008 Td_chr2.txt
    108  105624  425572 Td_chr3.txt
     92   89976  362806 Td_chr4.txt
    123  120294  484419 Td_chr5.txt
     77   75306  304010 Td_chr6.txt
     98   95844  386396 Td_chr7.txt
     63   61614  249078 Td_chr8.txt
     61   59658  241221 Td_chr9.txt
     54   52812  213823 Td_chr10.txt
    960  938880 3785195 total


Here is my brief description of what this code does

'mkdir' created a directory to carry out the experiment further; 
ran the 'awk' command with 'for' and 'i' loop to find ZMPIL, ZMPJA, ZMPBA, in the joined file
using the 'cut' command, all the words in the joined file that are ZMPIL, ZMPJA, ZMPBA were cut and transfered to a new file to do further data processing
'sort -k3,3n teosinte.txt > teosinte_sort.txt'  command was used to sort the header according the given position of SNP_ID, Chromosome and position
'grep' command was used to count the number of chromosomes and the number of times each chromosome appeared
'head -n 1' and 'awk' command was used to count 10 files (1 for each chromosome) with SNPs ordered based on increasing position values and separate each chromosomes in their respective files
'sed' stream editor command was used again to change the ? symbol to - hyphen, and separate them in a new file
(head -n 1 Teosinte_allhyphen.txt && tail -n +2 Teosinte_allhyphen.txt | sort -k3,3nr) > Teosinte_decreasingall10.txt  - this code was used to sort the maize files in decreasing order
'head -n 1' and 'awk' command was used to count 10 files (1 for each chromosome) with SNPs ordered based on decreasing position values and separate each chromosomes in their respective files
