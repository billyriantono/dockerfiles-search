FROM  snizhok/laravel-phantom-sphinx

RUN echo "#update image"
RUN apt-get update && apt-get install -y bash

RUN echo "#update php to 7.1"
USER root
RUN echo "# Set the locale"
#RUN update-locale LC_ALL=en_US.UTF-8 LANG=en_US.UTF-8
RUN apt-get clean && apt-get update
#&& apt-get install -y locales
#RUN locale-gen en_US.UTF-8
RUN apt-get install language-pack-en -y
RUN export LC_ALL=en_GB.UTF-8
RUN export LANG=en_GB.UTF-8
RUN LC_ALL=en_GB.UTF-8 LANG=en_GB.UTF-8 add-apt-repository -y -u ppa:ondrej/php
RUN apt-get clean && apt-get update
RUN apt-get install php7.1 php7.1-cli php7.1-xml php7.1-curl php7.1-common php7.1-json php7.1-opcache php7.1-mysql php7.1-mbstring php7.1-mcrypt php7.1-zip php7.1-fpm -y

RUN service php7.0-fpm stop
RUN service php7.1-fpm start
RUN service nginx restart

#RUN echo "#Install ES 7.3"

#FROM elasticsearch:7.3.0
#RUN chown -R :elasticsearch /usr/share/elasticsearch/data
#ENV discovery.type single-node
#EXPOSE 9200

