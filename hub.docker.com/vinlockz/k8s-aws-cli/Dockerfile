FROM ubuntu:latest

WORKDIR /var/app

COPY run.sh ./

RUN apt-get update -y
RUN apt-get install -y curl
RUN apt-get install -y awscli
RUN curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
RUN chmod +x ./kubectl
RUN mv ./kubectl /usr/local/bin/kubectl

CMD ["/bin/bash"]
