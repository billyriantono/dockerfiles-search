FROM python:3-slim

ENV PYTHONUNBUFFERED 1

RUN echo "flask" >> requirements.txt
RUN pip install --upgrade pip && pip install --no-cache-dir -r requirements.txt

WORKDIR /app

ADD main.py .

CMD ["env","FLASK_APP=main.py","flask","run"]
ENTRYPOINT ["python"]
