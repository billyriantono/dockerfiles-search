FROM ubuntu:18.04

RUN apt-get update && apt-get -y install wget rapidjson-dev openssl1.0 libssl1.0-dev libssl1.0.0 libcurl4 libcurl3-gnutls autoconf gnupg2

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 3FA7E0328081BFF6A14DA29AA6A19B38D3D831EF \
	&& echo "deb https://download.mono-project.com/repo/ubuntu stable-bionic main" | tee /etc/apt/sources.list.d/mono-official-stable.list \
	&& apt-get update \
    && apt-get install -y mono-devel mono-complete mono-xbuild

RUN apt-get install -y openjdk-8-jdk openjdk-8-jre maven

ENV JAVA_HOME   /usr/lib/jvm/java-8-openjdk-amd64/

RUN apt-get install -y python3-pip

RUN pip3 install pytest \   
    && pip3 install pytest-xprocess \
    && pip3 install sphinxcontrib-blockdiag \
    && pip3 install sphinxcontrib-seqdiag \
    && pip3 install sphinx_rtd_theme

RUN mkdir -p /usr/share/plantuml/ && wget https://search.maven.org/maven2/net/sourceforge/plantuml/plantuml/1.2019.8/plantuml-1.2019.8.jar -O /usr/share/plantuml/plantuml.jar
