FROM python:2.7-alpine
LABEL maintainer="1091354206@qq.com"
RUN pip install flask
WORKDIR /app
COPY . /app/
EXPOSE 5000
ENTRYPOINT [ "python", "app.py" ]
