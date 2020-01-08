FROM microsoft/aspnetcore:1.1
LABEL maintainer "yue@hemamaps.com.au"
RUN apt-get update \
    && curl -sL https://deb.nodesource.com/setup_8.x | /bin/bash - \
    && apt-get install -y nodejs \
        build-essential \
		g++ \ 
		flex \ 
		bison \ 
		gperf \ 
		ruby \ 
		perl \
        bzip2 \
        fontconfig \ 
		libsqlite3-dev \ 
		libfontconfig1-dev \ 
		libicu-dev \ 
		libfreetype6 \ 
		libssl-dev \ 
		libpng-dev \ 
		libjpeg-dev \ 
		python \ 
		libx11-dev \ 
		libxext-dev