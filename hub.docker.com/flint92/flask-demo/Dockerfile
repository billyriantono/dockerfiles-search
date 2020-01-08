FROM python:3.7
LABEL maintainer="1992flint@gmail.com"
COPY app.py /app/
WORKDIR /app
RUN pip3 install flask redis
EXPOSE 5000
CMD ["python", "app.py"]
