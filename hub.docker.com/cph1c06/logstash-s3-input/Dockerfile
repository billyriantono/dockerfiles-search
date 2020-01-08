FROM docker.elastic.co/logstash/logstash:7.3.2
RUN /usr/share/logstash/bin/logstash-plugin install logstash-input-s3 logstash-filter-grok
RUN /usr/share/logstash/bin/logstash-plugin update
RUN curl http://geolite.maxmind.com/download/geoip/database/GeoLite2-City.tar.gz --output GeoLite2-City.tar.gz
RUN tar -xvzf ./GeoLite2-City.tar.gz --strip-components 1
RUN rm ./GeoLite2-City.tar.gz
RUN rm ./README.txt
RUN rm ./LICENSE.txt
RUN rm ./COPYRIGHT.txt
RUN curl https://geolite.maxmind.com/download/geoip/database/GeoLite2-ASN.tar.gz --output GeoLite2-ASN.tar.gz
RUN tar -xvzf ./GeoLite2-ASN.tar.gz --strip-components 1
RUN rm ./LICENSE.txt
RUN rm ./COPYRIGHT.txt
