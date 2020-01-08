FROM openjdk:latest

ENV DOWNLOAD_URL "http://mirrors.advancedhosters.com/apache//directory/apacheds/dist/2.0.0.AM25/apacheds-2.0.0.AM25.tar.gz"


RUN cd /opt \
    && wget ${DOWNLOAD_URL} \
    && tar -zxvf $(find apacheds*.tar.gz) \
	&& rm $(find apacheds*.tar.gz) \
	&& mv apacheds* apacheds
	
WORKDIR /opt/apacheds

VOLUME /opt/apacheds/instances

EXPOSE 10389:10389 10636:10636 

ENTRYPOINT ["/opt/apacheds/bin/apacheds.sh", "default"]
CMD "run"
