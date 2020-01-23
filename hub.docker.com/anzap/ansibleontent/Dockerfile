FROM ubuntu:16.04

# Update
RUN apt-get -yqq update
RUN apt-get install -yqq python 
RUN apt-get -yqq install python-pip
RUN apt-get install sqlite3 libsqlite3-dev

# Install app dependencies
RUN pip install Flask
#RUN pip install -r requirements.txt

# Bundle app source
COPY app.py /app.py

EXPOSE  5000
#CMD ["python", "/app.py", "-p 5000"]
CMD ["python", "app.py"]
