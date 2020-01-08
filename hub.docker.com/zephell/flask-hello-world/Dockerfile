FROM frolvlad/alpine-python2
ENV PYTHONUNBUFFERED 1
RUN apk update
RUN apk add libxml2-dev
RUN mkdir /code
WORKDIR /code
ADD requirements.txt /code/
RUN pip install -r requirements.txt
ADD . /code/
EXPOSE 5000
CMD ["python", "main.py"]