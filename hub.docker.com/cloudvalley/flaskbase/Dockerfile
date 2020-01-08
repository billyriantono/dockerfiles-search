FROM cloudvalley/pabase:latest
LABEL maintainer Waylon Wang <waylon.act@gmail.com>

COPY requirements.txt requirements.txt

RUN pip install --upgrade pip \
    && pip install -r requirements.txt 

CMD ["python3"]
