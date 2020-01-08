FROM ubuntu

 
MAINTAINER 'Furkan Simsek '

 
RUN \
echo "****** Install Update and package  ******  " && \
apt-get update && apt-get install -y  && \
echo "****** ifconfig Install  ******  " && \
apt-get install net-tools -y && \
echo "****** Ping Install  ******  " && \
apt-get install iputils-ping -y  && \
echo "****** Zip  Install ******" && \
apt-get install zip -y && \
echo "****** Unzip  Install ******" && \
apt-get install unzip -y && \
echo "****** SSH   Install ******" && \
apt install openssh-server -y  && \
echo "****** Wget Install ******"&& \
apt-get install wget -y  && \
echo "****** Nano & Vim  Install ******"&& \
apt-get install nano  vim  -y  && \
echo "****** Firewal Install ******" && \
apt-get install firewalld -y 

CMD ["/bin/bash"]
