FROM python:3.6

WORKDIR /app

COPY requirements.txt /app/
COPY constraints.txt /app/

RUN pip install -r requirements.txt -c constraints.txt

COPY server.py /app/

CMD ["python", "server.py"]
