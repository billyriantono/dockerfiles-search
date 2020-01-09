FROM ubuntu:18.04

RUN apt-get update && \
    apt-get -y upgrade && \
    apt-get install -y  software-properties-common && \
    # add-apt-repository ppa:webupd8team/java -y && \
    # apt-get update && \
    # echo oracle-java7-installer shared/accepted-oracle-license-v1-1 select true | /usr/bin/debconf-set-selections && \
    # apt-get install -y oracle-java8-installer && \
    # apt-get clean
    apt install -y default-jdk
### 2. Get Java via the package manager
### 3. Get Python, PIP
RUN apt-get -y upgrade python3
RUN add-apt-repository -y ppa:deadsnakes/ppa
RUN apt install -y python3.7
RUN set -xe \
    && apt-get -y update \
    && apt-get -y install python-pip \
    && apt-get remove -y python3-pip; apt-get install -y python3-pip \
    && pip3 install virtualenv

COPY requirements.txt /

RUN pip3 install -r /requirements.txt

COPY . /app

WORKDIR /app
ENV PYTHONPATH "${PYTHONPATH}:/optimisation"

VOLUME [ "my-vol" ]

ENTRYPOINT ["/usr/bin/python3", "-m", "scoop","optimisation/algorithms/nsga_ii.py"]
CMD [""]
