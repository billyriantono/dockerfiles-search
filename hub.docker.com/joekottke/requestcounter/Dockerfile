FROM alpine:3.8
RUN apk add --no-cache python3 py3-pip
RUN mkdir /app
COPY src/requestcounter.py /app
COPY src/requirements.txt /app
WORKDIR /app
RUN pip3 install --no-cache-dir -r requirements.txt
EXPOSE 5555
CMD [ "python3", "./requestcounter.py" ]
