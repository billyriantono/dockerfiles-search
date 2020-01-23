FROM alpine as git
WORKDIR /work
RUN apk update && apk add git
RUN git clone https://github.com/p8ul/postman2apiary.git postman2apiary

FROM python:3.7.3-slim as python
WORKDIR /work
COPY --from=git /work /root
ENTRYPOINT ["python", "/root/postman2apiary/app/run.py"]