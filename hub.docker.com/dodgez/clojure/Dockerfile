FROM ubuntu:latest

RUN apt-get update -y && apt-get upgrade -y && \
  apt-get install -y openjdk-8-jre && \
  export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64 && \
  export PATH=$PATH:$JAVA_HOME/bin
RUN apt-get install -y curl rlwrap && \
  curl -O https://download.clojure.org/install/linux-install-1.10.1.489.sh && \
  chmod +x linux-install-1.10.1.489.sh && \
  ./linux-install-1.10.1.489.sh
RUN rm linux-install-1.10.1.489.sh
RUN apt-get install -y leiningen
