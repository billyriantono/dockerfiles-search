FROM continuumio/anaconda3

###################
# BASE
###################
RUN echo "deb http://http.us.debian.org/debian/ testing non-free contrib main" >> /etc/apt/sources.list

RUN apt-get update -y
RUN apt-get install -y zsh htop iftop ca-certificates netcat nano vim wget curl unzip bzip2

RUN apt-get install -y gcc

RUN apt-get install -y mediainfo
RUN bash -c "ln -sf /usr/bin/mediainfo /usr/local/bin/mediainfo"
#cpu bench tool
RUN apt-get install -y stress
#disk bench tool
RUN apt-get install -y hdparm
#network bench tool
RUN apt-get install -y iperf3

# for oracle
RUN apt-get install -y libaio1

# REQUIRE FOR loudness-corrector
RUN apt-get install -y libc6 libsndfile1

###################
# GOSU
###################
ENV GOSU_VERSION 1.7
RUN set -x \
    && apt-get update && apt-get install -y --no-install-recommends ca-certificates wget && rm -rf /var/lib/apt/lists/* \
    && wget -O /usr/local/bin/gosu "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture)" \
    && wget -O /usr/local/bin/gosu.asc "https://github.com/tianon/gosu/releases/download/$GOSU_VERSION/gosu-$(dpkg --print-architecture).asc" \
    && export GNUPGHOME="$(mktemp -d)" \
    && gpg --keyserver ha.pool.sks-keyservers.net --recv-keys B42F6819007F00F88E364FD4036A9C25BF357DD4 \
    && gpg --batch --verify /usr/local/bin/gosu.asc /usr/local/bin/gosu \
    && rm -r "$GNUPGHOME" /usr/local/bin/gosu.asc \
    && chmod +x /usr/local/bin/gosu \
    && gosu nobody true
    # \
    # && apt-get purge -y --auto-remove ca-certificates wget



###################
# ORACLE CLIENT & sqlplus & cxOracle STUFF
###################

ENV ORACLE_HOME /opt/oracle/instantclient_11_2
ENV LD_RUN_PATH=$ORACLE_HOME
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:$ORACLE_HOME
ENV PATH=$PATH:$ORACLE_HOME

RUN wget -O /tmp/instantclient-basic-linux.x64-11.2.0.4.0.zip "https://github.com/fingul/ansible-role-oracle-11g-client/blob/master/files/instantclient-basic-linux.x64-11.2.0.4.0.zip?raw=true"
RUN wget -O /tmp/instantclient-sdk-linux.x64-11.2.0.4.0.zip  "https://github.com/fingul/ansible-role-oracle-11g-client/blob/master/files/instantclient-sdk-linux.x64-11.2.0.4.0.zip?raw=true"
RUN wget -O /tmp/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip "https://github.com/fingul/ansible-role-oracle-11g-client/blob/master/files/instantclient-sqlplus-linux.x64-11.2.0.4.0.zip?raw=true"

RUN ls /tmp/

RUN \
	mkdir -p /opt/oracle && \
	unzip "/tmp/instantclient*.zip" -d /opt/oracle
RUN rm -f "/tmp/instantclient*.zip"

RUN ln -s $ORACLE_HOME/libclntsh.so.11.1 $ORACLE_HOME/libclntsh.so
RUN pip install cx_Oracle

###################
# loudness-corrector
###################

RUN wget -P /usr/local/bin/ "https://bitbucket.org/fingul/docker-loudness_validator-build/raw/master/bin/loudness-analyser"
RUN wget -P /usr/local/bin/ "https://bitbucket.org/fingul/docker-loudness_validator-build/raw/master/bin/loudness-corrector"
RUN bash -c "chmod +x /usr/local/bin/loudness-*"
RUN bash -c "ldd /usr/local/bin/loudness-*"


###################
# FFMPEG
###################

#FFMPEG_VERSION IS PLACEHOLDER FOR REDOWNLOAD BINARIES
ENV FFMPEG_VERSION 3.1.2
ENV LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/lib

RUN wget -O /usr/local/lib/libebur128.so.1 "https://github.com/fingul/sffmpeg/blob/master/lib/libebur128.so.1.1.0?raw=true"
RUN wget -O /usr/local/bin/frmxtract "https://github.com/fingul/sffmpeg/blob/master/bin/frmxtract?raw=true"
RUN wget -O /usr/local/bin/ffmpeg "https://github.com/fingul/sffmpeg/blob/master/bin/ffmpeg?raw=true"
RUN wget -O /usr/local/bin/ffprobe "https://github.com/fingul/sffmpeg/blob/master/bin/ffprobe?raw=true"
RUN bash -c "chmod +x /usr/local/bin/{ffmpeg,ffprobe,frmxtract}"
RUN bash -c "ldd /usr/local/bin/{ffmpeg,ffprobe,frmxtract}"

#RUN bash -c "chmod +x /usr/local/bin/{loudness-corrector,loudness-analyser,ffmpeg,ffprobe,frmxtract}"
#RUN bash -c "ldd      /usr/local/bin/{loudness-corrector,loudness-analyser,ffmpeg,ffprobe,frmxtract}"


# #
# #
# ##https://denibertovic.com/posts/handling-permissions-with-docker-volumes/
# #COPY entrypoint.sh /usr/local/bin/entrypoint.sh
# #ENTRYPOINT ["/usr/local/bin/entrypoint.sh"]
# #WORKDIR /code
# #
# #
