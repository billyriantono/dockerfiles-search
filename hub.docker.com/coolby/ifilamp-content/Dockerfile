FROM python:3.6.7
WORKDIR /app
COPY ./requirements.txt /app
RUN pip install --no-cache-dir -r requirements.txt
VOLUME /app/src
#RUN curl -O "https://convmind-models.s3.us-east-2.amazonaws.com/basic-models/data.tar" && \
#    tar -xvf data.tar
COPY . .
EXPOSE 9876
CMD [ "gunicorn", "-b", "0.0.0.0:9876", "-w", "4", "wsgi:application"]
