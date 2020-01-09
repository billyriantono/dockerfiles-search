FROM ubuntu
RUN apt-get update
RUN apt-get -y install python
COPY index.html /index.html
EXPOSE 8000
ENTRYPOINT ["python","-m","SimpleHTTPServer","8000"]
