FROM python:3
RUN mkdir /app && chmod 777 /app
ADD __main__.py /app
ADD requirements.txt /app
ADD _version.py /app
ADD run.sh /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["/app/run.sh"]
