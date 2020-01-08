FROM dclong/jdk

RUN echo "deb https://dl.bintray.com/sbt/debian /" >> /etc/apt/sources.list.d/sbt.list \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823

RUN apt-get update -y \
    && apt-get install -y \
        scala sbt \
    && apt-get autoremove \
    && apt-get autoclean 

