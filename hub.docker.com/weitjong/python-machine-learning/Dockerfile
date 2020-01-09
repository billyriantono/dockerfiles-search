FROM tiangolo/python-machine-learning:python3.7

LABEL maintainer="Yao Wei Tjong <weitjong@gmail.com>"

RUN conda install -y mysql-connector-python flask pandas numpy gunicorn && \
	apt-get update && apt-get install -y dnsutils
