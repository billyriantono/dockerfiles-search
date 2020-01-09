FROM ubuntu

MAINTAINER Anthony Roscio "@roscioa"

RUN apt-get update && apt-get -y -q install vim python3 git-core python-dev sudo build-essential gcc curl

RUN mkdir source

RUN cd source
RUN git clone git://git.drogon.net/wiringPi



CMD ["/bin/bash"]