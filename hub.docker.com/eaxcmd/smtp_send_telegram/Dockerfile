FROM python:3.7.6-alpine3.10

RUN pip install requests

EXPOSE 5566:5566

VOLUME ["/data"]

WORKDIR /data

COPY . /data

ENTRYPOINT ["python3", "/data/main.py"]

CMD ["-sp=SMTPPORT", "-bt=BOTTOKEN", "-ci=CHATID"]
