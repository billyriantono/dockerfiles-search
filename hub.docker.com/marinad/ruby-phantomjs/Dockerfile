FROM marinad/ruby
LABEL maintainer="denis.kiselyov@gmail.com"

RUN wget -q https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    tar jxf phantomjs-2.1.1-linux-x86_64.tar.bz2 && \
    cp phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin && \
    rm -rf phantomjs-2.1.1-linux-x86_64/ phantomjs-2.1.1-linux-x86_64.tar.bz2

RUN apt-get update -q && apt-get upgrade -y && apt-get install -y ghostscript
RUN rm -rf /var/lib/apt/lists/*
