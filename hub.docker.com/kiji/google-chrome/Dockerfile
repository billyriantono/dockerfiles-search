from centos:latest
COPY google-chrome.repo /etc/yum.repos.d/google-chrome.repo

RUN yum info google-chrome-stable && \
	yum install -y google-chrome-stable

RUN useradd -r chrome
USER chrome

ENTRYPOINT ["/usr/bin/google-chrome"]
CMD [ "--user-data-dir=/data" ]
