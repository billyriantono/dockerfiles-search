FROM adoptopenjdk/openjdk10
RUN apt-get update \
	&& apt-get upgrade -y \
        && apt-get --yes install xmlstarlet xsltproc wget unzip \
        && mkdir /openjfx \
        && cd /openjfx \
        && wget https://download2.gluonhq.com/openjfx/11.0.1/openjfx-11.0.1_linux-x64_bin-sdk.zip \
        && unzip openjfx-11.0.1_linux-x64_bin-sdk.zip 

