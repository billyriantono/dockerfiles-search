FROM redis:alpine
FROM python:3.4-alpine
EXPOSE 5000
ADD . /code
WORKDIR /code
RUN pip install -r requirements.txt
CMD python app.py
