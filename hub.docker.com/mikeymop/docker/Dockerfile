FROM kalilinux/kali-linux-docker
MAINTAINER Michael DeFrancesco <midefran@outlook.com>

RUN apt-get update
RUN apt-get -y upgrade

RUN apt-get -y install metasploit-framework

RUN sh -c "service postgresql start"
RUN sh -c "msfdb init"

CMD ["msfconsole"]
