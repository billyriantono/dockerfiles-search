# Set the base image to Ubuntu
FROM python:3.4-alpine

MAINTAINER cgarciaarano@gmail.com

# Update the repository sources list
RUN apk update && apk add git openssh-client

# Add requirements
COPY requirements.txt /opt/app/

WORKDIR /opt/app

# Install Python packages and system build dependencies
RUN pip install -r requirements.txt && \
	rm -rf /var/cache/apk/*

# Copy code
COPY * /opt/app/
ENTRYPOINT ["/usr/local/bin/python", "stashcli.py"]
CMD ["--help"]