FROM python:3.7-alpine

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /usr/src/app

COPY . .

EXPOSE 5000
ENTRYPOINT ["gunicorn"]
CMD ["--workers=2", "--bind=0.0.0.0:5000", "app:app"]
