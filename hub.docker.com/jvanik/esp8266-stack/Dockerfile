FROM eclipse/stack-base:ubuntu
RUN sudo apt-get update && \
    sudo apt-get -y install make unrar-free autoconf automake libtool gcc g++ gperf flex bison texinfo gawk ncurses-dev libexpat-dev python-dev python python-serial sed git unzip bash help2man wget bzip2 libtool-bin && \
    sudo apt-get clean
RUN git clone --recursive https://github.com/pfalcon/esp-open-sdk.git && \
    cd esp-open-sdk && \
    make STANDALONE=n && \
    sudo mv xtensa-lx106-elf /opt && \
    sudo chown -R root:root /opt/xtensa-lx106-elf && \
    cd .. && \
    rm -rf esp-open-sdk
