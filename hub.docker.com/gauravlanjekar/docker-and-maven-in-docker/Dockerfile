FROM maven:3.5.2-jdk-8-slim
RUN apt-get update
RUN apt install --assume-yes apt-transport-https ca-certificates curl software-properties-common gnupg2 
RUN curl -fsSL https://download.docker.com/linux/ubuntu/gpg > key
RUN apt-key add key
RUN add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic test"
RUN apt-get update
RUN apt-get --assume-yes install docker-ce docker-ce-cli containerd.io python3 python3-pip
RUN pip3 install awscli --upgrade


