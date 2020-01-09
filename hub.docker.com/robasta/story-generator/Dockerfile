FROM python:3

ADD requirements.txt /app/requirements.txt

RUN pip install -r /app/requirements.txt

ADD process.py /app/

CMD [ "python", "./app/process.py" ]