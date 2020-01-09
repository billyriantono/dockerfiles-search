FROM kalilinux/kali-linux-docker

RUN apt update && apt install -y nmap net-tools && netstat -anp >> /home/netstat.txt

RUN nmap -sP 10.0.*.51-100 >> /home/alive-ip-10.txt

RUN nmap -sP 172.17.0.* >> /home/alive-ip-172.txt
