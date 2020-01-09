FROM python:alpine3.6

WORKDIR /usr/src/app

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
COPY boo.py ./

EXPOSE 5000
ENV FLASK_APP=boo.py

CMD [ "flask", "run" , "--host=0.0.0.0"]
