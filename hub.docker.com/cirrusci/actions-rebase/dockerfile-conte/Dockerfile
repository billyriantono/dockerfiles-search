# https://github.com/elastic/elasticsearch-docker
FROM docker.elastic.co/elasticsearch/elasticsearch:5.2.2

# Add your elasticsearch plugins setup here
# Example: RUN elasticsearch-plugin install analysis-icu

# http://www.kwangsiklee.com/ko/2017/02/%EC%97%98%EB%9D%BC%EC%8A%A4%ED%8B%B1%EC%84%9C%EC%B9%98-5-2-0%EC%97%90-%EC%9D%80%EC%A0%84%ED%95%9C%EB%8B%A2-%EC%84%A4%EC%B9%98%ED%95%98%EA%B8%B0/
USER root
RUN apk update && \
	  apk add g++ wget make automake autoconf tar gzip openjdk8-jre-base

# mecab-ko 라이브러리 설치 [s]
COPY src/mecab-0.996-ko-0.9.2 /tmp/mecab-0.996-ko-0.9.2
WORKDIR /tmp/mecab-0.996-ko-0.9.2
RUN chown elasticsearch:elasticsearch /tmp/mecab-0.996-ko-0.9.2
RUN ./configure && \
		make && \
		make check && \
		make install
# mecab-ko 라이브러리 설치 [e]

# mecab-ko-dic 사전 설치 [s]
COPY src/mecab-ko-dic-2.0.1-20150920 /tmp/mecab-ko-dic-2.0.1-20150920
WORKDIR /tmp/mecab-ko-dic-2.0.1-20150920
RUN ./autogen.sh && \
		./configure && \
		make && \
		make install
# mecab-ko-dic 사전 설치 [e]

# Mecab.jar 설치 [s]
COPY src/mecab-java-0.996 /tmp/mecab-java-0.996
WORKDIR /tmp/mecab-java-0.996
ENV JAVA_HOME /usr/lib/jvm/default-jvm
ENV JAVA_TOOL_OPTIONS -Dfile.encoding=UTF8
RUN make && \
    cp libMeCab.so /usr/local/lib && \
    cp MeCab.jar /usr/local/lib && \
    chown -R elasticsearch:elasticsearch /usr/local/lib/libMeCab.so && \
    chown -R elasticsearch:elasticsearch /usr/local/lib/MeCab.jar && \
    chown -R elasticsearch:elasticsearch /usr/local/lib/*mecab*
ENV LD_LIBRARY_PATH /usr/local/lib:$LD_LIBRARY_PATH
# Mecab.jar 설치 [e]

# analysis-mecab-ko 플러그인 설치 [s]
# https://www.evernote.com/l/AK64eTNPmEdMj7xYjSaVG1yKr_mlJ00PBrg
COPY src/elasticsearch-analysis-mecab-ko-5.2.2.0 /usr/share/elasticsearch/plugins/elasticsearch-analysis-mecab-ko
# analysis-mecab-ko 플러그인 설치 [e]

#https://github.com/docker-library/elasticsearch/issues/111
RUN sysctl -w vm.max_map_count=262144

COPY /config /usr/share/elasticsearch/config
USER elasticsearch
WORKDIR /usr/share/elasticsearch
