FROM python:3.6.3

COPY requirements.txt .
RUN pip install -r requirements.txt 

COPY ./app /app

EXPOSE 5000

ENTRYPOINT ["python", "app/app.py"]
