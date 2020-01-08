FROM python:2

COPY requirements.txt /tmp
WORKDIR /tmp
RUN pip install -r requirements.txt

COPY . .

RUN ["tar", "xvf", "./dataset.tar.gz", "./prepared"]

RUN ["echo", "Started running dataset matching!"]
ENTRYPOINT ["/bin/bash", "./run.sh"]

CMD ["python", "-m", "SimpleHTTPServer", "8000"]