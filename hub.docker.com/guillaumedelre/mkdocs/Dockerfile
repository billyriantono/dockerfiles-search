FROM python:3.7-alpine

RUN apk add bash
RUN pip install --upgrade pip

ADD requirements.txt /tmp
RUN pip install --no-cache-dir -r /tmp/requirements.txt
RUN rm /tmp/requirements.txt

RUN mkdir -p /project/docs
ADD mkdocs.yml /project

WORKDIR /project

EXPOSE 8000

ENTRYPOINT ["mkdocs"]

CMD ["serve", "--dev-addr=0.0.0.0:8000"]
