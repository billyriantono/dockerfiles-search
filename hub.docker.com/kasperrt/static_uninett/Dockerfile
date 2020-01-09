FROM nginx

WORKDIR /srv/www

ADD default.conf /etc/nginx/conf.d/default.conf

RUN apt-get update && apt-get install -y curl npm python2.7 git
RUN cd /tmp && curl -LOk http://ftp.ruby-lang.org/pub/ruby/2.2/ruby-2.2.5.tar.gz && \
	tar -xvzf ruby-2.2.5.tar.gz && \
	cd ruby-2.2.5/ && \
	./configure --prefix=/usr/local && \
	make && \
	make install && \
	rm -rf ruby-2.2.5.tar.gz && \
	rm -rf ruby-2.2.5
RUN ln -s `which nodejs` /usr/bin/node
RUN rm -rf /var/lib/apt/lists/*

RUN gem install jekyll --no-ri --no-rdoc
RUN gem install rouge --no-ri --no-rdoc


EXPOSE 80
EXPOSE 443
