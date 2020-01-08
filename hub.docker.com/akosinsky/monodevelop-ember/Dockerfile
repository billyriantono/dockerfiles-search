FROM flexberry/mono-ember:1.0.0

ENV LANG ru_RU.UTF-8

COPY MonoDevelopProperties.xml /root/.config/MonoDevelop/7.0/MonoDevelopProperties.xml

RUN	apt-get install -y monodevelop mono-xsp4 locales mate-terminal
RUN	echo "LANG=ru_RU.UTF-8" > /etc/default/locale ; echo "ru_RU.UTF-8 UTF-8" > /etc/locale.gen ; \
	dpkg-reconfigure --frontend=noninteractive locales

CMD [ "/bin/bash" ]
