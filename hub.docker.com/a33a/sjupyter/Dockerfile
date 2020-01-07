FROM ubuntu:latest

RUN apt-get -y update

RUN apt-get -y install python3-pip net-tools

RUN apt-get -y install graphviz libgraphviz-dev

RUN pip3 install --upgrade pip

RUN pip3 install jupyter

RUN pip3 install numpy scipy matplotlib

RUN pip3 install ipyparallel

RUN ipcluster nbextension enable

ENV XDG_RUNTIME_DIR=""

CMD /bin/bash 
