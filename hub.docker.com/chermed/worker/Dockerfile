FROM python:3-alpine3.10
LABEL maintainer="Mohamed Cherkaoui <chermed@gmail.com>"
LABEL type="Worker"
RUN pip3 install redis==3.3.11 arrow==0.15.5
COPY ./app.py /app/
WORKDIR /app/
EXPOSE 5000
CMD ["python3", "app.py"]