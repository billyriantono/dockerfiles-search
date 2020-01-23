FROM dclong/tdodbc

RUN apt-get update \
    && apt-get install -y \
        gcc g++ \
        python3 python3-pip \
        python3-dev python3-setuptools python3-wheel

RUN pip3 install \
        teradata \
        pandas

