FROM ubuntu:17.10

RUN apt-get -y update
RUN apt-get -y install default-jdk ant python git build-essential

RUN git clone https://github.com/facebook/buck.git
WORKDIR buck

RUN ant

ENV PATH "$PATH:/buck/bin"

ENTRYPOINT ["/buck/bin/buck"]
