FROM python:3.4.4
 
RUN pip install -U pip
RUN pip install -U falcon
 
EXPOSE 8080
 
COPY . /hello-app
WORKDIR /hello-app
 
CMD ["python", "app.py"]
