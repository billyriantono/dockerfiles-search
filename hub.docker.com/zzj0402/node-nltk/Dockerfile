FROM node
RUN apt-get update
RUN apt-get install -y python3-pip locales locales-all
RUN pip3 install nltk requests numpy
RUN python3 -m nltk.downloader all
RUN locale-gen en_US en_US.UTF-8
RUN dpkg-reconfigure locales
RUN sed -i -e 's/# en_US.UTF-8 UTF-8/en_US.UTF-8 UTF-8/' /etc/locale.gen && \
    locale-gen
ENV LC_ALL en_US.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8 