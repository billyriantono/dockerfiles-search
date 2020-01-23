FROM python:3
RUN pip3 install mysql-connector;
ADD ./server-lte /
EXPOSE 80
ENTRYPOINT python3 -u ./main.py