FROM shellphish/mechaphish

USER root

RUN apt-get update && apt-get dist-upgrade -y && \
    apt-get install -y byacc bison flex texinfo build-essential gcc g++ git libncurses5-dev libmpfr-dev pkg-config libipt-dev libbabeltrace-ctf-dev coreutils g++-multilib && \
    mkdir -p /opt && cd /opt && git clone https://gitlab.com/akihe/radamsa.git && \
    cd radamsa && make -j`nproc` && mkdir -p /opt/radamsa_install && sed -i 's|DESTDIR=|DESTDIR=/opt/radamsa_install|g' ./Makefile && \
    make install
