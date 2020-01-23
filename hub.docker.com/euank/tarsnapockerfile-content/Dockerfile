FROM python:3.6-alpine

WORKDIR www

COPY ./ ./

ENTRYPOINT ["python", "-m", "http.server", "80"]
