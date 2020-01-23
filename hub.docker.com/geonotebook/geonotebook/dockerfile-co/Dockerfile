FROM openjdk:8-jdk

Maintainer gebobox <geobox@geo.top>

RUN curl -sL https://deb.nodesource.com/setup_8.x | bash - && \
    apt-get install -y nodejs bc && \
    wget -nv http://dl.bintray.com/sbt/debian/sbt-0.13.15.deb && \
    dpkg -i sbt-0.13.15.deb && \
    wget -nv http://www.scala-lang.org/files/archive/scala-2.12.4.deb && \
    dpkg -i scala-2.12.4.deb && \
    rm sbt-0.13.15.deb scala-2.12.4.deb && \
    sbt --version \
    apt-get clean

CMD sbt
