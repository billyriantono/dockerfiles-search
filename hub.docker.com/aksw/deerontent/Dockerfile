#install apache-php and base OS 
FROM ulsmith/alpine-apache-php7

#set environmental variables
ENV TZ=Europe/Budapest
ENV SUMO_HOME=/app/sumo-1.3.0
ENV SIMHOME=/app/simulation
ENV WEBS=/app/public/webs

#set timezone
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone


RUN apk add --update 
RUN apk add py3-matplotlib py3-numpy py3-flask py3-tabulate --update-cache --repository http://dl-3.alpinelinux.org/alpine/edge/testing/ --allow-untrusted
RUN apk add --no-cache \
	python3 \
	python3-dev \
	wget \
        git \
	py3-pip \
	screen 

#install the needed tools for simulation
WORKDIR /app/
RUN mkdir simulation \
	&& wget https://sumo.dlr.de/releases/1.3.0/sumo-src-1.3.0.tar.gz \
	&& tar -xzf sumo-src-1.3.0.tar.gz && rm sumo-src-1.3.0.tar.gz 

RUN git clone https://akos222:9f03b2b40768e57f0a009fe03a57779fd7975765@github.com/akos222/sim-toolkit.git

WORKDIR /app/sim-toolkit/

RUN chmod +x install.sh \
	&& sh install.sh 

WORKDIR /app/

RUN rm -r sim-toolkit


#add our web interface
WORKDIR /app/public/
RUN git clone https://akos222:9f03b2b40768e57f0a009fe03a57779fd7975765@github.com/akos222/webs.git && chmod -R 777 webs
RUN sed -i 's/Require\ all\ denied/Require\ all\ granted/g' /etc/apache2/httpd.conf
RUN chown -R apache:apache /app/
RUN httpd -k restart



