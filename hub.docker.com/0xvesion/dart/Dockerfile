FROM debian:stretch-slim

RUN apt update
RUN apt -yq install wget unzip git

RUN cd /tmp
RUN wget https://storage.googleapis.com/dart-archive/channels/stable/release/2.3.1/sdk/dartsdk-linux-x64-release.zip
RUN unzip dartsdk-linux-x64-release.zip
RUN rm dartsdk-linux-x64-release.zip
RUN mv dart-sdk /dart

RUN ln -s /dart/bin/dart /usr/local/bin/dart
RUN ln -s /dart/bin/dart2aot /usr/local/bin/dart2aot
RUN ln -s /dart/bin/dart2js /usr/local/bin/dart2js
RUN ln -s /dart/bin/dartanalyzer /usr/local/bin/dartanalyzer
RUN ln -s /dart/bin/dartaotruntime /usr/local/bin/dartaotruntime
RUN ln -s /dart/bin/dartdevc /usr/local/bin/dartdevc
RUN ln -s /dart/bin/dartdoc /usr/local/bin/dartdoc
RUN ln -s /dart/bin/dartfmt /usr/local/bin/dartfmt
RUN ln -s /dart/bin/pub /usr/local/bin/pub
RUN ln -s /dart/bin/snapshots /usr/local/bin/snapshots
RUN ln -s /dart/bin/utils /usr/local/bin/utils
