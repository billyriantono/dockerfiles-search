FROM java:8-jre

MAINTAINER kurow3 <kurow3 [at] dev.skurow.com>

ENV GITBUCKET_VER 4.20.0
ADD https://github.com/gitbucket/gitbucket/releases/download/${GITBUCKET_VER}/gitbucket.war /opt/gitbucket.war

COPY gitbucket.sh /opt/gitbucket.sh

RUN ln -s /gitbucket /root/.gitbucket

VOLUME /gitbucket

EXPOSE 8080 29418

CMD ["/opt/gitbucket.sh"]

