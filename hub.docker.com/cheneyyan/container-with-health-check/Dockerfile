FROM python:3.6-alpine
RUN mkdir -p /root/
COPY health /root
COPY ping /root
EXPOSE 3000 
WORKDIR /root

CMD python -m http.server 3000
