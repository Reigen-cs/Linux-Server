## 1. Finding Files

When working with Linux, you may not always have access to a graphical user interface. Typically, you'll interact with a terminal on a remote machine via SSH. Therefore, mastering specific commands to efficiently locate files, folders, or even search for text within files is crucial.

### Exercises 
1. Create a file named `my-file.txt` using the touch command. Then execute the `locate my-file.txt` command. Did you find the file?  
   > Your response: no
2. Run the command `sudo updatedb`. Execute `locate my-file.txt` again. Was the file found this time?  
   > Your response: yes
3. Use the `which` command to find the executable file for `nc` and provide its path.  
   > Path: /bin/nc
4. Use the `which` command to locate the executable file for `becode`. What is the flag?  
   > Command: `which becode`    
   > Flag: BC{WH1CH_FL4G_EXECUTLE_FILE}
5. Search for a file containing the name "Edgar Allan Poe" using the `find` command. What is the flag?  
   > Command: `find / -type f -exec grep -l "Edgar Allan Poe" {} + 2>/dev/null`  
   > Flag: BC{3d54r_4ll4n_P03_FL45}
6. Using the `find` command, locate the file `password.txt` and specify the flag.  
   > Command: `find / -name "password.txt" 2>&-`   
   > Flag: BC{PASSWORD_FILE}
7. With the `find` command, search for a file that starts with `becode-` and ends with `.sh`.  
   > Command: `find / -name "becode-*" 2>&-`   
   > Flag: BC{FLAG_FIND_PARTIAL_PATH}
8. Use the `find` command to identify files (not directories) modified in the last day and not owned by the root user. Execute `ls -l` on them. **Chaining/piping commands is NOT allowed!**  
   > Your command: `find / -type f -mtime -1 -print ! -user root`
9. Find all files with permissions set to `0777` using the `find` command.  
   > Your command: `find / -type f -perm 0777`
10. Use the `find` command to locate all files in the folder `/home/student/findme/` that have permissions set to `0777` and change their permissions to `0755`.  
    > Your command: `find /home/student/findme/ -type f -perm 0777 -exec chmod 0755 {} \;`
