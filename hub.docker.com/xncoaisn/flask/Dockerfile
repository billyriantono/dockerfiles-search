FROM python:3.8.0

RUN mkdir /app
WORKDIR /app

COPY requirements.txt ./

RUN pip install -r requirements.txt

COPY . .

EXPOSE 5000
CMD ["python", "app.py"]

