FROM python

RUN pip install -q flask requests pyyaml

MAINTAINER Gaël Lambert <gael.lambert@cycloid.io>
COPY ./receiver.py /receiver.py

EXPOSE 5000

CMD ["/receiver.py"]
