FROM jsums/msf-openvas-conda
MAINTAINER Ashley Abraham "ashley.abraham@jsums.edu"

ENV DEBIAN_FRONTEND noninteractive
ENV PYCHARM_HOME=/etc/pycharm

RUN apt-get -qq -y install \
    openjdk-8-jre \
    libxrender1 \
    libxtst6 \
    --no-install-recommends 
       
RUN curl -sSL https://download.jetbrains.com/python/pycharm-community-2018.2.4.tar.gz -o /tmp/pycharm-community.tar.gz \
    && mkdir ${PYCHARM_HOME} \
    && tar -xzvf /tmp/pycharm-community.tar.gz -C ${PYCHARM_HOME} --strip=1 
    
#RUN rm -rf /tmp/* \
#    && apt-get -qq -y autoremove \
#    && apt-get autoclean \
#    && rm -rf /var/lib/apt/lists/* /var/log/dpkg.log     

# Attach this container to stdin when running, like this:
# docker run --net=host -t -i jsums/msf-openvas-conda-pycharm
#--net=host allows listening to incoming connections on the host ip

ADD ./init.sh /init.sh
RUN chmod +x /init.sh
ENTRYPOINT ./init.sh
