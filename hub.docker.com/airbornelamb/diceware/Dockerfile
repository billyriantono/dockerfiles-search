#FROM python:3.7-alpine
FROM frolvlad/alpine-python3
COPY . /app/
WORKDIR /app
EXPOSE 8500
CMD ["python", "-m", "http.server", "8500"]
