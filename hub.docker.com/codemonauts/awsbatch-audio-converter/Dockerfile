FROM ubuntu:bionic

# Needed for apt-add-repository
RUN apt-get update && apt-get install --no-install-recommends -y software-properties-common apt-utils

RUN add-apt-repository ppa:chris-needham/ppa &&\
    apt-get update &&\
    apt-get install --no-install-recommends -y audiowaveform ffmpeg python3-pip python3-setuptools bc sox curl

RUN pip3 install ffmpeg-normalize awscli

COPY entrypoint.sh /bin/entrypoint.sh
COPY convert.sh /bin/convert.sh

CMD /bin/entrypoint.sh
