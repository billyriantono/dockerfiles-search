FROM java:8 

ADD http://mirrors.ukfast.co.uk/sites/ftp.apache.org/lucene/solr/5.2.1/solr-5.2.1.zip /solr.zip
RUN apt-get install -y unzip
RUN unzip solr.zip && rm solr.zip
RUN mv solr-5.2.1 solr
WORKDIR /solr
