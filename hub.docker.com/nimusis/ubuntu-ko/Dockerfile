FROM ubuntu:16.04
 			 
RUN apt-get update && \
    apt-get -y dist-upgrade && \
    apt-get autoremove -y && \
    apt-get clean all

RUN apt-get install -y language-pack-ko
RUN apt-get install tzdata
			 
# set locale ko_KR
RUN locale-gen ko_KR.UTF-8

ENV LANG ko_KR.UTF-8
ENV LANGUAGE ko_KR.UTF-8
ENV LC_ALL ko_KR.UTF-8

# Change timezone
RUN rm /etc/localtime
RUN ln -s /usr/share/zoneinfo/Asia/Seoul /etc/localtime

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /root

CMD /bin/bash
