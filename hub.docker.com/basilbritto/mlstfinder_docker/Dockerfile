FROM basilbritto/emmtyping_docker
MAINTAINER Basil Britto <basilbritto.xavier@uantwerpen.be>

WORKDIR /NGStools/mlstfinder

RUN apt update && apt install unzip

RUN wget https://bitbucket.org/genomicepidemiology/mlst_db/get/035f642871f6.zip
RUN unzip 035f642871f6.zip
