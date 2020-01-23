FROM python:3
ENV PYTHONUNBUFFERED 1

ADD . /tmp
WORKDIR /tmp

# Installa tutti i requisiti Ubuntu
RUN apt-get update
RUN apt-get --assume-yes install `cat apt-dependencies.txt | grep -v "#" | xargs`

# Scarica e installa i requisiti PIP da CroceRossaItalian/jorvik (branch master)
RUN pip install -r https://raw.githubusercontent.com/CroceRossaItaliana/jorvik/master/requirements.txt
