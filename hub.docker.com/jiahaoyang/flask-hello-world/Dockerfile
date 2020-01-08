FROM python:2.7
MAINTAINER jiahaoyang "jiahao_yang@qq.com"
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD [ "python", "app.py" ]
