FROM python:3.6.8-slim-stretch

RUN apt-get update && apt-get install -y \
	build-essential \
	make \
	gcc \
	locales \
	libgomp1 \
	libgdal20 libgdal-dev && \
	python3 -m pip install numpy==1.15.4 && \
	python3 -m pip install scipy==1.2.0 && \
	python3 -m pip install pandas==0.23.4 && \
	python3 -m pip install scikit-learn==0.20.2 && \
	python3 -m pip install xgboost==0.81 && \
	rm -r /root/.cache/pip && \
	apt-get remove -y --purge libgdal-dev make gcc build-essential && \
	apt-get autoremove -y && \
	rm -rf /var/lib/apt/lists/*
