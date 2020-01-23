FROM ubuntu:16.04

MAINTAINER chen1i6c04 <chen1i6c04@gmail.com>

RUN apt-get update -qq && \
	apt-get install -y -qq \
	git \
	blast2 \
	make \
	curl && \
	git clone https://bitbucket.org/genomicepidemiology/resfinder.git && \
	cd resfinder && \
	git clone https://bitbucket.org/genomicepidemiology/resfinder_db.git && \
	mv resfinder_db database && \
	rm -rf /var/cache/apt/* /var/lib/apt/lists/*;

RUN curl -L https://cpanmin.us -k | perl - App::cpanminus && \
	cpanm Try::Tiny::Retry && \
	cpanm CJFIELDS/BioPerl-1.6.924.tar.gz --force && \
	cpanm File::Temp;
	




