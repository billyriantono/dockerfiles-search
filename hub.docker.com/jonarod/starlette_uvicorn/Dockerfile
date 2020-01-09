# Start with a tiny minimalist 27MB linux image and python 3.6+
FROM python:3.6.7-alpine3.7

RUN apk update && apk upgrade && pip install -U pip

#RUN apk add --update alpine-sdk make gcc python3-dev python-dev libxslt-dev libxml2-dev libc-dev openssl-dev libffi-dev zlib-dev py-pip openssh \
#    && rm -rf /var/cache/apk/*

RUN apk add --update make gcc python3-dev libc-dev \
    && rm -rf /var/cache/apk/*

# install python dependencies
RUN pip install starlette uvicorn

# Add basic binaries to $PATH to use commands like 'bash', 'cat'... directly without specifying entire path
ENV PATH /bin:/usr/local/bin:$PATH

# Install users' packages
# CMD pip install -r /home/dependencies.txt

# Launch server.py
# CMD pip install -r /home/dependencies.txt && python /home/server.py
ENTRYPOINT ["/bin/sh", "-c", "pip install -r /home/dependencies.txt && python /home/server.py"]

# open default 8000 port
EXPOSE 8000

