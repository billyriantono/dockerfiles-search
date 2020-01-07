FROM mtvaught/cron-base:latest

RUN apk update && \
	apk add python py-pip && \
	pip install configparser youtube-dl

RUN mkdir -p /root/staging

COPY sample.ini      /root/staging/sample.ini
COPY startup-root.sh /root/staging/startup.sh
COPY program.sh      /root/staging/run.sh
COPY download.py     /root/staging/download.py

RUN chmod +x /root/staging/startup.sh

RUN sh -n /root/staging/startup.sh
RUN sh -n /root/staging/run.sh
RUN python -m py_compile /root/staging/download.py

#CMD ["su", "-c", "bash", "-l", "user"];
