FROM python:alpine

LABEL maintainer="misterfifi"

RUN touch requirements.txt
RUN pip install -r requirements.txt

COPY . /opt/app/

EXPOSE 5000

ENTRYPOINT ["python", "/opt/app/app.py"]
