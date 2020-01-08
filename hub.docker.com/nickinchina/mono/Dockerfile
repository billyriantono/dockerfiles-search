FROM mono:latest
    
RUN mozroots --machine --import --sync --quiet \
    && curl -o /root/Npgsql.dll http://ftp1.s2konline.net/t/Npgsql.dll \
    && rm -rf /usr/lib/mono/gac/Npgsql && gacutil -i /root/Npgsql.dll && rm /root/Npgsql.dll \
    	&& apt-get remove -y curl \
	&& apt-get autoremove -y \
	&& apt-get clean

RUN apt-get update
RUN apt-get install -y make
RUN apt-get install -y gcc
RUN apt-get install -y libxslt-dev libxml2-dev
RUN apt-get install -y wget git-core

ADD run.sh /root/run.sh
RUN chmod +x /root/run.sh
EXPOSE 8000 80
