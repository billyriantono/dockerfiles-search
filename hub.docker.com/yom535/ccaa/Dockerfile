FROM yom535/systemd-ssh-ubuntu

RUN apt-get update
RUN apt-get install -y wget unzip curl make net-tools iproute2 iputils-ping iptables
RUN wget https://github.com/yompc/ccaa/archive/master.zip -O /root/master.zip
WORKDIR /root
RUN unzip master.zip
WORKDIR /root/ccaa-master
RUN chmod +x ccaa.sh
RUN chmod +x upbt.sh
RUN wget https://github.com/yompc/Student_Management_System_2018/raw/master/bbr30080.sh -O /root/bbr.sh

ENTRYPOINT /bin/bash /root/ccaa-master/ccaa.sh & /bin/bash /root/bbr.sh & /usr/sbin/sshd -D
