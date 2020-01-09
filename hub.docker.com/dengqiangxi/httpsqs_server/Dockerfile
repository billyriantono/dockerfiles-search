FROM ubuntu

RUN softwares='apt-utils net-tools iputils-ping gcc make libz-dev libbz2-dev libreadline6-dev' && apt-get update && apt-get install -y $softwares && rm -rf /var/lib/apt/lists/*
WORKDIR /root/
COPY  ./httpsqs_libs/  .
RUN ["/bin/bash","-c","./install.sh"]
EXPOSE 80

CMD ["/usr/bin/httpsqs","-p","80","-x","/data/queue","-a","auth"]
