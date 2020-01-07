FROM shippableimages/ubuntu1404_base:latest

RUN apt-get update && apt-get install -y \
    ca-certificates \
    curl software-properties-common;

# Install a default nodejs for the system
RUN curl -sL https://deb.nodesource.com/setup_4.x | sudo -E bash -

RUN apt-get update

RUN apt-get install --yes nodejs
RUN apt-get install python-dev -y
RUN pip install ansible

CMD ["node"]
