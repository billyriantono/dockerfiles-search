FROM python:3.6
LABEL maintainer "Sam Mackenzie <sam.mackenzie@live.com>"
COPY . /app
WORKDIR /app
RUN pip install -r requirements.txt
ENTRYPOINT ["python"]
CMD ["run.py"]
EXPOSE 80
