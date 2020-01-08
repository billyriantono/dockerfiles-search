FROM williamyeh/ansible:alpine3

RUN apk add --no-cache \
		python2-dev

RUN pip install --upgrade \
		pip

WORKDIR /root
COPY requirements.txt .

RUN pip install --upgrade \
		-r requirements.txt

WORKDIR /work
VOLUME  /work

