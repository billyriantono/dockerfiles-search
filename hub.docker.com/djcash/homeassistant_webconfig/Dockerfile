FROM python:3.5

MAINTAINER Charley <2555085@gmail.com>

WORKDIR /root

COPY configurator.py /root/configurator.py

VOLUME ["/config"]
EXPOSE 3218

CMD ["python","/root/configurator.py"]