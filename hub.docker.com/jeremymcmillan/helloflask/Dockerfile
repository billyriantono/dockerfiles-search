FROM python:3-alpine as flask
RUN apk add --no-cache curl

COPY . /
WORKDIR /Flask
RUN pwd
RUN find .
RUN pip install -r requirements.txt

FROM flask as hello_app
WORKDIR Hello/app
ENV FLASK_APP hello.py
RUN pwd && find / -name $FLASK_APP && ls -lF $FLASK_APP
RUN python -m flask run --reload --eager-loading& sleep 1 && curl -vvv 'http://localhost:5000' && echo; kill $!

FROM scratch
COPY --from=flask / /

COPY --from=hello_app /Flask/Hello/app/ /

LABEL author="Jeremy McMillan <jeremy.mcmillan@gmail.com>"
ENV FLASK_APP hello.py
WORKDIR /Flask/Hello/app
RUN python -m flask routes
EXPOSE 5000/tcp
ENTRYPOINT ["python", "-m", "flask"]
CMD ["run", "--host", "0.0.0.0"]
