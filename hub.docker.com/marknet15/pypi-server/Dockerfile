FROM alpine:3.7

LABEL maintainer="Mark Woolley <mw@marknet15.com>"
LABEL version="0.1"
LABEL description="Simple PyPi Server Docker Image"

# Install required package
RUN apk add --update --no-cache py-pip && \
    pip install --upgrade pip && \
    pip install pypiserver && \
    mkdir /packages

# Expose port to be published
EXPOSE 8080

# Create exposed volume
VOLUME ["/packages"]

# Add entrypoint
ADD entrypoint.sh /
RUN chmod a+x entrypoint.sh

# Run Pypi server
CMD ["/entrypoint.sh"]