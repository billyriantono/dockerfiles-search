FROM python:3

MAINTAINER Richard Weber <tebro@tebro.fi>
ADD run.sh /run.sh
RUN chmod +x /run.sh
WORKDIR /src

ENTRYPOINT ["/run.sh"]
CMD ["app.py"]
