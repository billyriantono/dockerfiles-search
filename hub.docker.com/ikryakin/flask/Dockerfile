FROM python:3.6

RUN apt-get update
ARG proxy
RUN export https_proxy=$proxy \
 && pip install flask \
 && unset https_proxy


ADD hello.py /tmp/hello.py

EXPOSE 5000

CMD ["python", "/tmp/hello.py"]

