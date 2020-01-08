FROM python:2.7
LABEL maintaner="wgw@gmail.com"
COPY . /app
WORKDIR /app
RUN pip install flask redis ipython
EXPOSE 5000
CMD python app.py
