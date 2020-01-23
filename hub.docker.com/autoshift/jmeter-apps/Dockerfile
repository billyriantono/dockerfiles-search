FROM hauptmedia/jmeter


# Install Python.
RUN \
  apt-get update && \
  apt-get install -y python python-dev python-pip python-virtualenv && \
  rm -rf /var/lib/apt/lists/*


RUN pip install flask

ENV PROVIDER rancher

COPY loader.py /loader.py
COPY Airports.csv /tmp/Airports.csv
COPY Airports2.csv /tmp/Airports2.csv
COPY start.sh /start.sh
RUN chmod +x /start.sh


CMD /start.sh
