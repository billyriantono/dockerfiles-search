FROM maven
COPY kuromoji-server /usr/src/app
WORKDIR /usr/src/app
RUN mvn install
RUN apt-get update \
 && apt-get install -y graphviz \
 && apt-get clean && rm -rf /var/lib/apt/lists/*
