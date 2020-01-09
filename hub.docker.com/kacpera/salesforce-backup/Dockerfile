FROM python:3.7-alpine

RUN mkdir -p /opt/salesforce/libs/
ADD libs/* /opt/salesforce/libs/
ADD requirements.txt sf-backup-to-s3.py /opt/salesforce/
RUN chmod +x /opt/salesforce/sf-backup-to-s3.py && \
  pip install -r /opt/salesforce/requirements.txt

WORKDIR /opt/salesforce/
CMD ["--help"]
ENTRYPOINT ["python", "sf-backup-to-s3.py"]
