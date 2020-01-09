FROM java:8-jre as build

ENV HUGOUP_VERSION 1.0.1
ADD https://dl.bintray.com/lorislab/maven/org/lorislab/hugoup/hugoup-assembly/$HUGOUP_VERSION/hugoup-assembly-$HUGOUP_VERSION-bin.zip /opt
RUN mkdir /opt/hugoup
RUN unzip /opt/hugoup-assembly-$HUGOUP_VERSION-bin.zip -d /opt/hugoup
RUN rm /opt/*.zip

ENV HUGO_VERSION 0.40.1
ADD https://github.com/gohugoio/hugo/releases/download/v$HUGO_VERSION/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz /opt
RUN mkdir /opt/hugo
RUN tar xvzf /opt/hugo_${HUGO_VERSION}_Linux-64bit.tar.gz -C /opt/hugo
RUN rm /opt/*.tar.gz

RUN mkdir -p /opt/www

FROM java:8-jre

COPY hugoup /root/.hugoup

COPY --chown=root:root --from=build /opt /opt
RUN ln -s /opt/hugoup/hugoup /usr/local/bin
RUN ln -s /opt/hugo/hugo /usr/local/bin

WORKDIR /opt/www

