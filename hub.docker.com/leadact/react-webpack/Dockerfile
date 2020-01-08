FROM node:12.10.0-stretch

RUN apt-get update && apt-get install -y \
	locales \
	git \
	curl \
	ruby-full \
	yarn \
	vim

# SASS/Compass
RUN gem install sass -v 3.4.18
RUN gem install compass

ADD entrypoint.sh /usr/bin/entrypoint.sh
CMD sh /usr/bin/entrypoint.sh
