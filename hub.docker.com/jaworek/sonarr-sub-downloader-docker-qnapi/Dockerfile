FROM linuxserver/sonarr

RUN echo "deb http://ppa.launchpad.net/krzemin/qnapi/ubuntu xenial main" > \
    	/etc/apt/sources.list.d/sonarr.list && \
     apt-get update && \
     apt-get install -y --allow-unauthenticated \
    	qnapi

COPY sub-downloader.sh /app/sub-downloader.sh

RUN chmod +x /app/sub-downloader.sh
