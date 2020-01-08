FROM wernight/phantomjs
MAINTAINER mcouto@gmail.com

USER root
COPY start.sh /
RUN mkdir /data && chmod 777 /data
WORKDIR /data

USER phantomjs
VOLUME [ "/data" ]
ENV PHANTOMJS_SCRIPT  script.js

CMD ["/start.sh"]
