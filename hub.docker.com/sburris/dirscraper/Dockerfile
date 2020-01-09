FROM alpine:latest

WORKDIR /opt/

ENV url https://www.google.com
ENV filename output.txt

RUN apk add --update py-pip git && \
	git clone https://github.com/Cillian-Collins/dirscraper.git

WORKDIR /opt/dirscraper/

RUN pip install -r requirements.txt
	
VOLUME /opt/output

ENTRYPOINT python /opt/dirscraper/dirscraper.py -d -u $url -o /opt/output/$filename