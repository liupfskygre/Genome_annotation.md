## this is a markdown file for the use of aai.rb from 
(https://github.com/lmrodriguezr/enveomics/tree/master/Scripts)



##draft bash.sh
```
#!/usr/bin/bash

#toadd
genome_list1=$1
genome_list2=$2

#call
#./aai_calculator_ruby.sh [genome_list1.txt] [genome_list2.txt]

for file1 in $(cat ${genome_list1}) #GCA_000008865.2_ASM886v2_protein.faa
do
for file2 in $(cat ${genome_list1}) #GCA_000008865.2_ASM886v2_protein.faa
do
echo ${file1}
echo ${file2}
~/aai.rb -1 ./${file1} -2 ./${file2} -T temp1.txt -p diamond -t 2 #-b /Users/pengfeiliu/anaconda3/envs/Diamond/bin
awk -F '\t' -v a="${file1}" -v b="${file2}" '{print a"\t"b"\t"$0}' temp1.txt>tmp2.txt
cat tmp2.txt>>final_two_way_AAI.txt
done
# paste header to the final results
done



```
