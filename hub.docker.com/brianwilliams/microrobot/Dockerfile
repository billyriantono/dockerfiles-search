FROM python:3-alpine
LABEL maintainer="Brian-Williams"

RUN mkdir -p /usr/src/app && \
    mkdir -p /home/testing/robot/
WORKDIR /usr/src/app

COPY requirements.txt /usr/src/app/

# Make sure python3 pathfile dir exists and add app to pythonpath
RUN pip3 install --no-cache-dir -r requirements.txt && \
    mkdir -p "$(python3 -m site --user-site)" && \
    echo "/usr/src/app/" > "$(python3 -m site --user-site)/api.pth"

COPY . /usr/src/app

EXPOSE 8080

ENTRYPOINT ["python3"]

CMD ["-m", "swagger_server"]