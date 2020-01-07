FROM openjdk

MAINTAINER smduarte (smd@fct.unl.pt)

RUN useradd -ms /bin/bash me

RUN apt-get update && \
	apt-get install -y python3 && \
	apt-get -y autoclean && apt-get -y autoremove  


ENV PYDEV=PyDev-5.3.0.zip
ENV ECLIPSE=eclipse-java-neon-R-linux-gtk-x86_64.tar.gz

WORKDIR /
COPY $ECLIPSE .

RUN tar xvfz $ECLIPSE && \
	rm -f $ECLIPSE && \	
	ls -al

WORKDIR eclipse/dropins

COPY $PYDEV .

RUN unzip $PYDEV && rm $PYDEV

WORKDIR /home/me
USER me

RUN mkdir workspace

ENV DISPLAY=10.0.0.1:0

CMD [ "/eclipse/eclipse", "-data", "/home/me/workspace"]