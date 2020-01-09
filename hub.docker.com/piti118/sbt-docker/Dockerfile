FROM java

RUN apt-get update
RUN apt-get upgrade -y
RUN apt-get install wget -y
RUN wget https://dl.bintray.com/sbt/debian/sbt-0.13.16.deb
RUN dpkg -i sbt-0.13.16.deb

#build some cache

WORKDIR /tmp
COPY . /tmp
RUN sbt update
