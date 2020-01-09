FROM python:3.5.1-alpine
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code
EXPOSE 8080
CMD python app.py
