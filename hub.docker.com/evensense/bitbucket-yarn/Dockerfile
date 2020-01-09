FROM atlassian/default-image:2

RUN npm install --global yarn
RUN apt-get update && apt-get install -y python-dev
RUN set -e ; \
	curl -O https://bootstrap.pypa.io/get-pip.py ; \
	python get-pip.py ; \
	rm get-pip.py
RUN pip install awscli

