## 3. Piping and Redirection

### Exercises

1. Write "hello everyone" to a file named "test" by redirecting the output of the `echo` command.  
   > Your command: `echo "hello everyone" > ./test`
2. Append "goodbye" to the same file "test" without overwriting its content, then verify using the `cat` command.  
   > Your command: `echo "goodbye" >> ./test`
3. Redirect the output of the `ls -la` command to a file named `foo`.  
   > Your command: `ls -al > foo`
4. Execute `find /etc -name *conf*` and redirect only error messages to a file named `err.txt`.  
   > Your command: `find /etc -name *conf* 2> err.txt`
5. Repeat the previous exercise, this time redirecting errors to Linux's null device.  
   > Your command: `find /etc -name *conf* 2> /dev/null`
6. Now redirect both standard output and error output of the `find /etc -name *conf*` command to separate files (`std.out` and `std.err`).  
   > Your command: `find /etc -name *conf* 2> errors.txt 1> output.txt`
7. Create a named pipe called "MyNamedPipe". Execute the `pwd` command to send data into this pipe, then use `cat` to read from "MyNamedPipe".  
   > Your commands: `mkfifo MyNamedPipe pwd > MyNamedPipe && cat MyNamedPipe`
8. Use the `cat` command to number the lines in `/etc/passwd` with the `nl` command.  
   > Your commands: `cat /etc/passwd | nl`
9. With the previous `nl` command, use `head` and `tail` to display lines from `/etc/passwd` between line 7 and line 12.  
   > Your commands: `nl /etc/passwd | head -n 11 | tail -n 4`
