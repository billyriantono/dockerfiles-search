FROM jenkins/jnlp-slave

USER root

RUN apt-get update && apt-get install wget -y && apt-get install tar -y

RUN wget https://dl.google.com/go/go1.12.7.linux-amd64.tar.gz && tar -C /usr/local -xzf go1.12.7.linux-amd64.tar.gz

ENV PATH=$PATH:/usr/local/go/bin:GOPATH=root/go

USER jenkins

ENTRYPOINT ["jenkins-slave"]
