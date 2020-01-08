FROM python:3.7.1-slim

RUN pip install --upgrade pip

COPY ./requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

CMD [ "/bin/bash" ]
