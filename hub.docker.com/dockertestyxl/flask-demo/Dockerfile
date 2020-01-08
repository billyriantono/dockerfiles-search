#test
FROM python:2.7
LABEL maintaner="Peng Xiao xiaoquwl@gmail.com"
WORKDIR /app
COPY app.py .
RUN pip install flask redis
EXPOSE 5000
CMD [ "python", "app.py" ]
