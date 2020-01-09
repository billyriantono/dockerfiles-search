FROM python:2.7-slim-stretch

RUN apt update
RUN apt install -y libxml2-dev \
			libxslt-dev \
			gcc \
			libpq-dev \
			libmariadbclient-dev

WORKDIR /lianjia-scrawler
ADD . /lianjia-scrawler

RUN pip install -r requirements.txt


