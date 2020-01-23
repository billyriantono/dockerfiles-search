FROM devopscenter/web_apache:0.1.1
MAINTAINER josh < josh [at] devops {dot} center>

ENV HOME /root
ENV IS_DOCKER True
ENV IS_WORKER True

ADD requirements.txt /requirements.txt
RUN cd / && pip install -r requirements.txt

RUN apt-fast -y install build-essential
RUN cd / && wget http://download.redis.io/releases/redis-2.8.13.tar.gz
RUN cd / && tar xvzf redis-2.8.13.tar.gz
RUN cd /redis-2.8.13 && make -j 3 && make install
RUN cd /redis-2.8.13 && \
mkdir -p /etc/redis && \
cp -f *.conf /etc/redis

CMD /etc/init.d/pgpool start && redis-server /etc/redis/redis.conf
