FROM python:3.4

RUN apt-get update -y && \
    apt-get upgrade -y && \
	apt-get install -y git build-essential libcurl4-gnutls-dev libgnutls28-dev python3-dev && \
	apt-get clean && \
	rm -rf /var/lib/apt/lists/ /tmp/ /var/tmp/*
	
RUN git clone https://github.com/certtools/intelmq.git /tmp/intelmq
WORKDIR /tmp/intelmq

RUN pip3 install -r REQUIREMENTS && pip3 install . 
RUN mv /opt/intelmq/etc/examples/*.conf /opt/intelmq/etc/
COPY config/* /opt/intelmq/etc/

RUN useradd -d /opt/intelmq -U -s /bin/bash intelmq && \
    chmod -R 0770 /opt/intelmq && \
    chown -R intelmq.intelmq /opt/intelmq

COPY intelmq_docker /usr/local/bin/

USER intelmq
WORKDIR /opt/intelmq
CMD ["sh", "/usr/local/bin/intelmq_docker"]
