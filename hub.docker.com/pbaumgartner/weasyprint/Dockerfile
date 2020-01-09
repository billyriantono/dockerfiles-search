FROM debian:buster
ENV PYTHONUNBUFFERED 1
RUN echo 'deb http://cdn-fastly.deb.debian.org/debian buster main contrib' > /etc/apt/sources.list
RUN apt-get update -y && \
    apt-get install -y build-essential python3-pip python3-cffi libcairo2 libpango-1.0-0 libpangocairo-1.0-0 libgdk-pixbuf2.0-0 libffi-dev shared-mime-info ttf-mscorefonts-installer --fix-missing && \
    rm -rf /var/lib/apt/lists/*
RUN pip3 install weasyprint
WORKDIR /data

ENTRYPOINT ["weasyprint"]