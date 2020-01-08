FROM suzlab/python:latest

RUN apt-get update
RUN apt-get install -y libfontconfig1 fonts-ipafont-mincho fonts-ipafont-gothic
RUN apt-get clean

RUN pip install selenium

WORKDIR /root

COPY .bashrc.patch ./
RUN patch .bashrc < .bashrc.patch
RUN rm .bashrc.patch

RUN curl -sOL https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN bunzip2 phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN tar xvf phantomjs-2.1.1-linux-x86_64.tar
RUN cp phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/
RUN rm phantomjs-2.1.1-linux-x86_64.tar 
RUN rm -R phantomjs-2.1.1-linux-x86_64 
