FROM python:3.4
LABEL maintainer="zjliuwei@126.com"
LABEL version="1.0"
LABEL description="This is description"
RUN pip install flask
ADD app.py /app.py
WORKDIR /
EXPOSE 5000
CMD python ./app.py

