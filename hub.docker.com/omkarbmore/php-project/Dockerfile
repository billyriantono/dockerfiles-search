FROM python:3-onbuild
RUN apt-get update
COPY . /usr/src/app
EXPOSE 8080
CMD ["python", "api.py"]

