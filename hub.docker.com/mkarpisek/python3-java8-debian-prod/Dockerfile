FROM bitnami/python:3.7

RUN apt-get update && \
	apt-get install --no-install-recommends -y software-properties-common && \ 
	add-apt-repository -y ppa:openjdk-r/ppa && \
	apt-get install --no-install-recommends -y openjdk-8-jre && \
	rm -rf /var/lib/apt/lists/*

COPY requirements.txt /requirements.txt
RUN pip install -r /requirements.txt

CMD ["python3"]
