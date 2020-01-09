FROM debian:stable

RUN apt-get update && apt-get install -y git python3 python3-pip && rm -rf /var/lib/apt/lists/*
RUN pip3 install awscli
RUN git clone https://github.com/nccgroup/ScoutSuite.git /opt/ScoutSuite

WORKDIR /opt/ScoutSuite

RUN pip3 install -r requirements.txt
ENTRYPOINT [ "python3", "scout.py" ]