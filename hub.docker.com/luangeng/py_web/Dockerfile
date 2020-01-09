FROM python:3.6-alpine
MAINTAINER lg "1057935399@qq.com"

WORKDIR /app

ADD . /app

RUN pip install -r requirements.txt

EXPOSE 80
ENV name luangeng

CMD ["python", "py_web.py"]
