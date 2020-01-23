FROM python:alpine

WORKDIR /usr/src/app
COPY ./code .
RUN pip install --no-cache-dir -r requirements.txt
EXPOSE 5000

CMD ["python", "app.py"]
