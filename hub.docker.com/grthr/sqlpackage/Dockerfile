FROM ubuntu:16.04

RUN apt-get update && apt-get install -y libunwind8 libicu55 wget unzip

RUN mkdir /opt/sqlpackage && \
  cd /opt/sqlpackage && \
  wget https://sqlpackage.blob.core.windows.net/daily/sqlpackage-linux-x64-latest.zip  && \
  unzip sqlpackage-linux-x64-latest.zip  && \
  rm sqlpackage-linux-x64-latest.zip && \
  chmod +x sqlpackage && \
  ln -s /opt/sqlpackage/sqlpackage /usr/local/bin/sqlpackage
