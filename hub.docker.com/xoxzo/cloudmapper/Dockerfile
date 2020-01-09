FROM python:3.7

COPY . /app
WORKDIR /app

RUN pip install -U pip && pip install -r requirements.txt

ENTRYPOINT ["python", "cloudmapper.py"]
CMD ["webserver", "--public"]
