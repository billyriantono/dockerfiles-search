# Sphinxsearch
#
# VERSION               0.0.1
FROM ubuntu
MAINTAINER Võ Anh Duy <anhduy@siliconstraits.vn>

RUN apt-get update
RUN apt-get -y install software-properties-common
RUN add-apt-repository -y ppa:builds/sphinxsearch-rel21 && apt-get update && apt-get install sphinxsearch -y

CMD [ "searchd", "--nodetach" ]

EXPOSE 9312
