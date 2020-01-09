# escape=`

FROM airdock/oracle-jdk

LABEL maintainer "unititled99@gmail.com"

RUN apt-get -y update && apt-get install -y unzip wget
RUN wget http://nlp.stanford.edu/software/stanford-corenlp-full-2016-10-31.zip
RUN unzip stanford-corenlp-full-2016-10-31.zip && `
    rm stanford-corenlp-full-2016-10-31.zip

WORKDIR stanford-corenlp-full-2016-10-31

ENTRYPOINT ["/srv/java/jdk/bin/java", "-cp", "*", "-mx4g", "edu.stanford.nlp.pipeline.StanfordCoreNLPServer"]
