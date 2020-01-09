FROM adoptopenjdk/openjdk8:alpine
LABEL maintainer="asiemer@gmx.de"

ENV ANT_VERSION=apache-ant-1.10.5
ENV ANT_BINARY=${ANT_VERSION}-bin.tar.gz
WORKDIR /tmp
RUN wget https://www.apache.org/dist/ant/binaries/${ANT_BINARY} ;\
  tar zxvf ${ANT_BINARY} ;\
  mv ${ANT_VERSION} /opt/ant
RUN adduser -D -g '' user; \
  mkdir /src ;\
  chown -R user:user /src
USER user
ENV PATH=${PATH}:/opt/ant/bin
WORKDIR /src

CMD ["ant", "-v"]
