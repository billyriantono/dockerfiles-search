FROM python:3

WORKDIR /usr/src/app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY script.py .

CMD ["python", "./script.py"]
EXPOSE 8000
