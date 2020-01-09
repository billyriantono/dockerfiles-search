FROM tiangolo/uwsgi-nginx:python3.7

LABEL maintainer="Rahul Shukla <shukla2009@gmail.com>"

# RUN pip install pipenv
    
# Place your flask application on the server
COPY requirement.txt /app
RUN pip install -r requirement.txt
COPY ./src /app/src
COPY ./data /app/data
WORKDIR /app
RUN mkdir models

EXPOSE 5002
CMD ["python","src/api/server.py"]
