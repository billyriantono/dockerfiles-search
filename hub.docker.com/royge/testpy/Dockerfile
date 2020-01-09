# Base image
FROM python:2.7

# Author
LABEL maintainer="Roy Evangelista <royevangelista@gmail.com>"

# Install test libraries
RUN pip install django-test-without-migrations==0.4 \
                mock==2.0.0 requests-mock==1.3.0 \
                factory_boy==2.9.2 moto==1.1.1

# Create volume mount point
RUN mkdir /app

# Define volume
VOLUME /app

# Change working directory
WORKDIR /app

# Entrypoint
ENTRYPOINT ["/app/entrypoint.sh"]
