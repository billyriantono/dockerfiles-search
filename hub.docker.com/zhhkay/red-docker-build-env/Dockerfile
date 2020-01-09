FROM ubuntu:14.04
ADD http://mirrors.163.com/.help/sources.list.trusty /etc/apt/sources.list
RUN apt-get update
RUN apt-get install -y make
RUN apt-get install -y g++
RUN apt-get install -y libboost-dev
RUN apt-get install -y thrift-compiler
RUN apt-get install -y openjdk-7-jdk
RUN apt-get install -y wget
ADD https://raw.githubusercontent.com/technomancy/leiningen/stable/bin/lein /usr/bin/
RUN chmod 755 /usr/bin/lein
RUN lein self-install
RUN apt-get clean
ADD https://raw.githubusercontent.com/zhang-heng/red/master/clojure/project.clj /
RUN lein deps
RUN rm project.clj
