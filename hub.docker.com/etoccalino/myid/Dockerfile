FROM python:3-alpine

WORKDIR /src

RUN pip install --no-cache-dir gunicorn falcon

COPY myid.py .

CMD ["gunicorn", "-b", "0:8080", "myid:api"]
