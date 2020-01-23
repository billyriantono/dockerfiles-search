FROM r-base:latest

MAINTAINER Andy Pohl "apohl@morgridge.org"

RUN cd /root && \
    wget http://cran.wustl.edu/src/base/R-3/R-3.0.2.tar.gz && \
    tar xfz R-3.0.2.tar.gz && \
    cd R-3.0.2/ && \
    ./configure --prefix=/opt --with-x=no && make && make install && \
    cd ../ && rm -rf R-3.0.2/
RUN /opt/bin/Rscript -e "install.packages('fdrtool', repos='http://cran.r-project.org')"

CMD ["/opt/bin/R"]
