FROM python:3.7.3-stretch

RUN pip install jupyter awscli tensorflow shapely pandas matplotlib boto3 sklearn image

COPY entrypoint /

CMD ["/entrypoint"]

