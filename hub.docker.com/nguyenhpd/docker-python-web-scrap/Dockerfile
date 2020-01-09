FROM python:3.6-jessie

RUN mkdir -p /var/python_scripts
RUN mkdir -p /var/python_scripts_executed
RUN mkdir -p /var/python_download

RUN apt-get update && \
  apt-get install -y --no-install-recommends \
  libxml2-dev \
  libxslt-dev \
  python-dev

RUN pip install lxml requests simplejson beautifulsoup4

WORKDIR /var/python_scripts
RUN chmod 755 /var/python_scripts

COPY entry_point.sh /usr/local/bin/entry_point.sh
RUN chmod +x /usr/local/bin/entry_point.sh

ENTRYPOINT ["/usr/local/bin/entry_point.sh"]