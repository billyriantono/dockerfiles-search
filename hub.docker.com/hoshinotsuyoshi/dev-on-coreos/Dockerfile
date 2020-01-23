FROM debian:sid
RUN apt-get update && \
    apt-get -y install wget build-essential && \
    export DIR=/opt && \
    mkdir -p $DIR/source && \
    cd $DIR/source && \
    wget "http://ftp.gnu.org/pub/gnu/ncurses/ncurses-5.9.tar.gz" && \
    tar xzvf ncurses-5.9.tar.gz && \
    cd ncurses-5.9 && \
    ./configure --prefix=$DIR --with-shared && \
    make && \
    make install && \
    cd .. && \
    wget "http://sourceforge.net/projects/zsh/files/zsh/5.0.2/zsh-5.0.2.tar.gz" && \
    tar xzvf zsh-5.0.2.tar.gz && \
    cd zsh-5.0.2 && \
    ./configure --prefix=$DIR --enable-cflags="-I$DIR/include" --enable-cppflags="-I$DIR/include" --enable-ldflags="-L$DIR/lib"  --enable-multibyte --enable-locale --with-tcsetpgrp && \
    make && \
    make install
RUN echo "cp -r /opt/bin/*     /target/bin/"     >  /install.sh && \
    echo "cp -r /opt/lib/*     /target/lib/"     >> /install.sh && \
    echo "cp -r /opt/share/*   /target/share/"   >> /install.sh && \
    echo "cp -r /opt/include/* /target/include/" >> /install.sh && \
    chmod +x /install.sh
CMD /install.sh
