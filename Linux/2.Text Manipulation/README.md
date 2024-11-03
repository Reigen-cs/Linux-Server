## 2. Text Manipulation

### Exercises
1. Search for all occurrences of "Loxondota" in `/home/student/lorem.txt`.  
   > Flag: BC{GREP_ME_LOREM_FL4G}
2. Copy the file `/etc/passwd` to your home directory. Display the line starting with the `student` name.  
   > Your commands:  
   > `cp /etc/passwd /home/student/`  
   > `grep -rn passwd -e "student"`
3. Display lines in the passwd file that start with login names of 3 or 4 characters.  
   > Your command: `awk -F: '{if(length($1) == 3 || (length($1) == 4)) print $1}' passwd`
4. In the file `/home/student/sample.txt`, how many unique values exist in the first and second columns?  
   > Your response: 4 in each column.  
   > Your command: `cut -d "," -f 1 /home/student/sample.txt | sort -u | wc -l`
5. In `/home/student/sample.txt`, sort the values in the second column by frequency of occurrence. (Use `uniq -c` if helpful).  
   > Your command: `cut -d "," -f 2 /home/student/sample.txt | sort | uniq -c | sort`
6. In `/home/student/iris.data`, change the column separator (comma) to tab (ensure the changes are applied to the file).  
   > Your command: `sed 's/,/\t/g' iris.data > iris.data.parsed`
7. In `/home/student/iris.data`, extract the third column (petal length in cm) using `cut`.  
   > Your command: `cut -f3 d$'\t' iris.data.parsed`
8. In `/home/student/iris.data`, count the number of unique flower species. (Use `cut` and `uniq`).  
   > Your response: 3  
   > Your command: `cut -f5 d$'\t' iris.data.parsed | uniq`
9. In `/home/student/iris.data`, sort by increasing petal length (consider sort options).  
   > Your command: `sort -k 3 iris.data.parsed`
10. In `/home/student/iris.data`, show only lines with petal lengths greater than the average size.  
    > Your command: `average=\`awk '{ total += $3 } END {print total/NR}' /home/student/iris.data\``
11. Using `/etc/passwd`, extract the user and home directory fields for all users on your student machine whose shell is set to `/bin/false`.  
    > Your command: `grep "/bin/false$" /etc/passwd | cut -d ":" -f 1,6`
