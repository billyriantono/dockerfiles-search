FROM pypy:3.6

ADD . /code/
WORKDIR /code
ADD requirements.txt /code/

RUN pypy3 -m ensurepip
RUN pip install --upgrade pip
RUN pip install -r requirements.txt
RUN pip install pycurl

EXPOSE 12378

ENTRYPOINT celery -A task worker --loglevel=info
CMD pypy3 app.py