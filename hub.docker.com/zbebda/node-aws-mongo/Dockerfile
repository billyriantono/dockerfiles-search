FROM node:8.10

RUN apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6 && \
    echo "deb http://repo.mongodb.org/apt/debian jessie/mongodb-org/3.4 main" | tee /etc/apt/sources.list.d/mongodb-org-3.4.list

RUN apt-get update && apt-get install -y \
    python-dev \
    zip \
    jq \
    mongodb-org-tools=3.4.10 \
    mongodb-org-shell=3.4.10 && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean
    
    
RUN curl -O https://bootstrap.pypa.io/get-pip.py

RUN python get-pip.py
RUN pip install awscli
