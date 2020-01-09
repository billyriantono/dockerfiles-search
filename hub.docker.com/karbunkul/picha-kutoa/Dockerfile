FROM debian
RUN apt-get update && apt-get install -y \
	curl \
	python \
	make \
	g++
RUN curl -sL https://deb.nodesource.com/setup_7.x | bash -
RUN apt-get update && apt-get install -y \
	nodejs
EXPOSE 5000