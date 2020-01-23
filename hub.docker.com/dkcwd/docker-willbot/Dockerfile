FROM python:2.7.11
RUN apt-get update -y && apt-get install -y python2.7-dev
RUN pip install will
RUN pip install lxml
RUN cd / && mkdir willbot && cd willbot && generate_will_project
