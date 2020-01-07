FROM daald/ubuntu32:trusty

#add openjdk-8-jdk
RUN sudo apt-get install -y software-properties-common && \
    sudo add-apt-repository ppa:openjdk-r/ppa && \
    sudo apt-get update -y && \
    sudo apt-get install -y openjdk-8-jdk && \
    sudo apt-get install -y openssh-server && \
    sudo apt-get clean

