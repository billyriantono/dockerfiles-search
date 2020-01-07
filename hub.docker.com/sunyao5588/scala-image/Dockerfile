FROM java:8

WORKDIR /app

# install sbt , curl git nodejs npm
RUN apt-get update -y \
    && apt-get install apt-transport-https -y \
    && echo "deb http://dl.bintray.com/sbt/debian /" | tee -a /etc/apt/sources.list.d/sbt.list \
    && apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 642AC823 \
    && apt-get update -y \
    && apt-get install sbt -y \
    && apt-get install curl git -y

# git checkout source code
RUN git clone https://yao.yc.sun:Init1234@gitlab.com/dsolutions/bitsearch.git \
    && cd bitsearch && git checkout steven\
    && sbt compile test \
    && cd .. && rm -rf ./bitsearch

# install play
RUN git clone https://github.com/playframework/play-scala-starter-example.git \
    && cd /app/play-scala-starter-example && sbt run && cd .. && rm -rf play-scala-starter-example

# install react
RUN curl -sL https://deb.nodesource.com/setup_10.x | bash - \
    && apt-get install nodejs -y \
    && npm install -g create-react-app \
    && create-react-app my-app \
    && cd my-app && npm run build

VOLUME ["/root/.ivy2"]
VOLUME ["/root/.sbt"]

CMD ["sbt", "-v"]

