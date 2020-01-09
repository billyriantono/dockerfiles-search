FROM apache/zeppelin:0.8.0
MAINTAINER Jose Sanchez <josegabriel.st@gmail.com>

RUN apt-get update && \
    apt-get install -y python3-pip && \
    rm -rf /var/lib/apt/lists/*

RUN pip3 install \
    numpy \
    pandas \
    scipy \
    scikit-learn

# Python 3
RUN sed -i '/"propertyName":\s"zeppelin\.python"/{n; s/python/python3/g}' /zeppelin/interpreter/python/interpreter-setting.json

