FROM ubuntu:trusty
MAINTAINER hax404 <hax404@hax404.de>

RUN apt-get update
RUN apt-get install --no-install-suggests --no-install-recommends -y wget
RUN wget --header='Host: softlayer-ams.dl.sourceforge.net' --header='User-Agent: Mozilla/5.0 (X11; Linux x86_64; rv:31.0) Gecko/20100101 Firefox/31.0' --header='Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8' --header='Accept-Language: en-US,en;q=0.5' --header='Referer: http://sourceforge.net/projects/pdfsandwich/files/pdfsandwich%200.1.3/pdfsandwich_0.1.3_amd64.deb/download' --header='Cookie: __utma=191645736.165154399.1412282132.1412282132.1412700359.2; __utmc=191645736; __utmz=191645736.1412700359.2.2.utmcsr=tobias-elze.de|utmccn=(referral)|utmcmd=referral|utmcct=/pdfsandwich/index.html; notice_preferences=2:; __utmb=191645736.7.9.1412700410257; __utmt_1=1; __utmt_2=1' --header='Connection: keep-alive' 'http://softlayer-ams.dl.sourceforge.net/project/pdfsandwich/pdfsandwich%200.1.3/pdfsandwich_0.1.3_amd64.deb' -O '/tmp/pdfsandwich_0.1.3_amd64.deb' -c
RUN apt-get install --no-install-suggests --no-install-recommends -y tesseract-ocr unpaper exactimage imagemagick ghostscript
RUN dpkg -i /tmp/pdfsandwich_0.1.3_amd64.deb
RUN apt-get install --no-install-suggests --no-install-recommends -y proftpd
RUN apt-get install --no-install-suggests --no-install-recommends -y inotify-tools
ADD proftpd.conf /etc/proftpd/proftpd.conf
RUN mkdir -p /tmp/scan/ocr && chmod 777 -R /tmp/scan
ADD start.sh /usr/local/start.sh
RUN chmod +x /usr/local/start.sh
ENTRYPOINT /usr/local/start.sh

