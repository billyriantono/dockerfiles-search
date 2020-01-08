FROM python:3.7.6-alpine3.10

RUN adduser -h /home/archive -D archive

# Install App
RUN pip3 install Flask==1.1.1
RUN pip3 install boto3==1.9.218

COPY src /home/archive
RUN chown -R archive:archive /home/archive && \
    chmod -R u=rwX,g=rX,o= /home/archive

# Configure app
EXPOSE 5000
ENV ARCHIVE_STORAGE_DRIVER=s3

# Setup run environment
USER archive:archive
WORKDIR /home/archive
ENTRYPOINT ["flask", "run", "-h", "0.0.0.0"]
