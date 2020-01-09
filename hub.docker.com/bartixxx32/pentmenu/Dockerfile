FROM ubuntu
RUN apt update
RUN apt upgrade -y
RUN DEBIAN_FRONTEND=noninteractive apt install bash sudo curl netcat hping3 openssl stunnel nmap whois host ike-scan net-tools -y
ADD pentmenu /
ENTRYPOINT ["./pentmenu"]
