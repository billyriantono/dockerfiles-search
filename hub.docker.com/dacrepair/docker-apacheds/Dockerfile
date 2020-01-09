FROM openjdk:alpine
MAINTAINER Derek Vance <DACRepair@gmail.com>


ENV DL_URL http://mirrors.sorengard.com/apache//directory/apacheds/dist/2.0.0.AM25/apacheds-2.0.0.AM25.tar.gz
ENV INSTANCE default

RUN wget -O /tmp/apacheds.tar.gz ${DL_URL}
RUN mkdir /usr/share/apacheds \
    && tar -zxf /tmp/apacheds.tar.gz -C /usr/share/apacheds --strip-components=1 \
    && rm /tmp/apacheds.tar.gz \
    && apk --no-cache add bash \
    && rm /usr/share/apacheds/bin/*.bat
    
WORKDIR /usr/share/apacheds

COPY entrypoint.sh /usr/share/apacheds/bin/
RUN chmod +x /usr/share/apacheds/bin/entrypoint.sh

EXPOSE 10389
EXPOSE 10636
EXPOSE 60088
EXPOSE 60464

ENTRYPOINT ["/usr/share/apacheds/bin/entrypoint.sh"]
CMD ["run"]
