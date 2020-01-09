FROM kalilinux/kali-linux-docker

RUN apt update && apt install -y nmap && apt install net-tools -y

RUN nmap -v -Pn -sV -O 172.17.0.1 >> /home/nmap-1.txt

RUN nmap -v -Pn -sV -O 172.17.0.2 >> /home/nmap-2.txt
