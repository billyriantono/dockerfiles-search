FROM debian

RUN apt-get update -y && \
    apt-get install -y git clang cmake make gcc g++ libmariadbclient-dev libssl-dev libbz2-dev libreadline-dev libncurses-dev libboost-all-dev mariadb-server p7zip default-libmysqlclient-dev && \
    update-alternatives --install /usr/bin/cc cc /usr/bin/clang 100 && \
    update-alternatives --install /usr/bin/c++ c++ /usr/bin/clang 100 && \
    git clone -b 3.3.5 --depth 1 git://github.com/TrinityCore/TrinityCore.git && \
    cd TrinityCore && mkdir build && cd build && cmake ../ -DCMAKE_INSTALL_PREFIX=/root/server && \
    make && make install

CMD /bin/bash
