# base image ubuntu
FROM ubuntu:16.04

LABEL Name="docker-nluml-local Version=0.0.1"
LABEL maintainer="Donny Seo <jams7777@gmail.com>"

# Install wget and install/updates certificates node
RUN apt-get update \
	&& apt-get install --no-install-recommends --no-install-suggests -y \
						ca-certificates ca-certificates-java bzip2 apt-transport-https \
						cron supervisor automake autotools-dev build-essential \
						gettext-base libelf1 \
						vim curl ssh git wget \
						libmecab2 libmecab-dev \
						openjdk-8-jdk \
						python3-pip python3-dev \
						libpq-dev \
	&& update-ca-certificates -f \
	&& cd /usr/local/bin \
    && ln -s /usr/bin/python3 python \
	&& rm -rf /var/lib/apt/lists/* \
	&& rm -rf /var/cache/oracle-jdk8-installer

ENV LC_ALL C.UTF-8
ENV LANG en_US.UTF-8
ENV LANGUAGE en_US.UTF-8

ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/
RUN export JAVA_HOME
RUN export LANG=en_US.UTF-8
RUN pip3 install --upgrade pip

# mecab
RUN wget -O - https://bitbucket.org/eunjeon/mecab-ko/downloads/mecab-0.996-ko-0.9.2.tar.gz | tar zxfv -
RUN cd mecab-0.996-ko-0.9.2; ./configure; make; make install; ldconfig

# dic
RUN wget -O - https://bitbucket.org/eunjeon/mecab-ko-dic/downloads/mecab-ko-dic-2.0.3-20170922.tar.gz | tar zxfv -
RUN cd mecab-ko-dic-2.0.3-20170922; sh ./autogen.sh
RUN cd mecab-ko-dic-2.0.3-20170922; ./configure; make; make install; ldconfig

# delete
RUN rm -rf /var/lib/apt/lists/*
RUN apt-get remove -y build-essential

# work dir make
RUN mkdir /app && chmod 777 -R /app
RUN mkdir /app/nlu_ml && chmod 777 -R /app/nlu_ml

RUN mkdir /app/files && chmod 777 -R /app/files
RUN mkdir /app/files/mecab-dic && chmod 777 -R /app/files/mecab-dic
RUN mkdir /app/files/mecab-dic/dic && chmod 777 -R /app/files/mecab-dic/dic
RUN mkdir /app/files/compared && chmod 777 -R /app/files/compared
RUN mkdir /app/files/compared/appattern && chmod 777 -R /app/files/compared/appattern
RUN mkdir /app/files/compared/similarity && chmod 777 -R /app/files/compared/similarity
RUN mkdir /app/files/compared/userdic && chmod 777 -R /app/files/compared/userdic
RUN mkdir /app/files/logbackup && chmod 777 -R /app/files/logbackup
RUN mkdir /app/files/logbackup/nlu && chmod 777 -R /app/files/logbackup/nlu

RUN mkdir /logs && chmod 777 -R /logs
RUN mkdir /logs/Backup && chmod 777 -R /logs/Backup
RUN touch /logs/nlu_ml.log && chmod 777 /logs/nlu_ml.log

# log setting
# RUN ln -sf /dev/stdout /logs/nlu_rule.log

# Install pip lib
COPY ./requirements.txt /root/requirements.txt
RUN chmod 777 /root/requirements.txt
RUN pip3 install setuptools
RUN pip3 install -r /root/requirements.txt
RUN pip3 install fuzzywuzzy[speedup]
RUN pip3 install https://github.com/JonathanRaiman/glove/archive/master.zip

RUN git clone https://github.com/facebookresearch/fastText.git /tmp/fastText
RUN rm -rf /tmp/fastText/.git*
RUN cd /tmp/fastText; pip3 install .

# nginx setting
#COPY ./nginx.conf /etc/nginx/nginx.conf
#COPY ./default.conf /etc/nginx/sites-enabled/default
#COPY ./package.json /app/web/package.json

# platform root
WORKDIR /app/nlu_ml

# exec shell setting
COPY ./start.sh /root/start.sh
RUN chmod 777 /root/start.sh

# alais setting
RUN  echo "alias logview='tail -100f /logs/nlu_ml.log'" >> /root/.bashrc
RUN  echo "alias app='cd /app/nlu_ml'" >> /root/.bashrc
RUN  echo "alias start='/root/start.sh'" >> /root/.bashrc

RUN  echo "echo " >> /root/.bashrc
RUN  echo "echo " >> /root/.bashrc
RUN  echo "echo ' ************     danbee.Ai nlu_ml Local [ local ]        ************* ' " >> /root/.bashrc
RUN  echo "echo ' *****                                                            ******* ' " >> /root/.bashrc
RUN  echo "echo ' ***** << Alias >>                                                ******* ' " >> /root/.bashrc
RUN  echo "echo ' *****      app  : nlu ml app                                     ******* ' " >> /root/.bashrc
RUN  echo "echo ' *****  logview  : nlu ml log                                     ******* ' " >> /root/.bashrc
RUN  echo "echo ' *****     start : start nlu ml                                   ******* ' " >> /root/.bashrc
RUN  echo "echo ' ************************************************************************ ' " >> /root/.bashrc

# Volume setting
VOLUME ["/app/nlu_ml"]

# Port setting
EXPOSE 8001

CMD ["/bin/bash"]
