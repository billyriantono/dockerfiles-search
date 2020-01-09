FROM python:3.6-stretch
ADD requirements.txt /tmp/requirements.txt
RUN pip install -r /tmp/requirements.txt
ADD . /code
WORKDIR /code
CMD ["flask", "run", "--host=0.0.0.0"]
