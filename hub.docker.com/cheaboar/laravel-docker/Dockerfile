FROM ubuntu:14.04
RUN apt-get update
RUN apt-get  install -y curl \
	nginx \
	wget \
	python-pip
ENV PATH /usr/local/nginx/bin:$PATH
COPY requirements.txt /tmp/
RUN pip install --requirement /tmp/requirements.txt
COPY . /tmp/
ENTRYPOINT ["chan"]
CMD ["--help"]
