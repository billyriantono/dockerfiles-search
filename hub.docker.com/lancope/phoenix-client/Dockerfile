FROM lancope/java:7-openjdk

RUN apt-get install -yq python wget

# phoenix
RUN wget -q -O - http://xenia.sote.hu/ftp/mirrors/www.apache.org/phoenix/phoenix-4.2.0/bin/phoenix-4.2.0-bin.tar.gz | tar -xz -C /usr/local/
RUN cd /usr/local && ln -s ./phoenix-4.2.0-bin phoenix

ENTRYPOINT ["/usr/local/phoenix/bin/sqlline.py"]
