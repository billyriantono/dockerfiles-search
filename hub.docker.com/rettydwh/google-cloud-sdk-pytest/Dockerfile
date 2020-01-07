FROM google/cloud-sdk:alpine

RUN curl https://bootstrap.pypa.io/get-pip.py > /tmp/get-pip.py \
	&& python /tmp/get-pip.py \
	&& pip install \
		pytest==3.1.2 \
		pytest-cov \
		pytest-pep8 \
		pytest-mock==1.6.2
