FROM ubuntu
RUN apt-get update
RUN apt-get install -y python
RUN echo 1.0 >> /etc/version && apt-get install -y git \
    && apt-get install -y iputils-ping

RUN mkdir /datos
WORKDIR /datos
RUN touch f1.txt

RUN mkdir /datos2
WORKDIR /datos2
RUN touch f2.txt

ENTRYPOINT ["/bin/bash"]