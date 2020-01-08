FROM google/cloud-sdk:latest

RUN apt-get -qqy update && apt-get install -qqy wget \
      python \
      python-dev \
      python3 \
      python3-dev

RUN wget https://bootstrap.pypa.io/get-pip.py
RUN python get-pip.py
RUN pip --version

RUN git clone https://github.com/hadv/python-docs-samples
WORKDIR /python-docs-samples/pubsub/cloud-client
RUN pip install -r requirements.txt
