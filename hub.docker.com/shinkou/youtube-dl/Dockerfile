FROM shinkou/python
RUN set -x \
	&& apt update\
	&& apt upgrade -y \
	&& apt install -y ffmpeg
RUN pip install --upgrade pip
RUN pip install youtube-dl
RUN wget https://bitbucket.org/ariya/phantomjs/downloads/phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN tar -jxvf ./phantomjs-2.1.1-linux-x86_64.tar.bz2 -C /usr/local/
RUN rm ./phantomjs-2.1.1-linux-x86_64.tar.bz2
RUN ln -s /usr/local/phantomjs-2.1.1-linux-x86_64/bin/phantomjs /usr/local/bin/
COPY docker-entrypoint.sh /usr/local/bin/
RUN ln -s /usr/local/bin/docker-entrypoint.sh /
ENTRYPOINT ["docker-entrypoint.sh"]
WORKDIR /data
CMD ["bash"]
