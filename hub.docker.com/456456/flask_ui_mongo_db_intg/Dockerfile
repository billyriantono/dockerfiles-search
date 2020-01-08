FROM ubuntu:16.04

# Install Python.
RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*
# Install app dependencies
RUN pip install Flask
RUN pip install pymongo
RUN pip install bson
#RUN pip install -r requirements.
# Bundle app source
COPY test.py /src/test.py
COPY templates  /src/templates
COPY static  /src/static

EXPOSE  8000
CMD ["python", "/src/test.py", "-p 8000"]

