FROM python:2.7-slim
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 80
CMD [ "python", "__main__.py", "-H 0.0.0.0" ]
