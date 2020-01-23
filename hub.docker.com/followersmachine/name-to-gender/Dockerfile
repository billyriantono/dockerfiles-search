FROM python:3

EXPOSE 5000
WORKDIR /app
ADD ./app/ /app/
RUN pip install --no-cache-dir -r requirements.txt

CMD ["python", "server.py"]