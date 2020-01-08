FROM alpine:3.1

# Update
RUN apk add --update python py-pip

# Install app dependencies
RUN pip install Flask
#RUN pip install -r requirements.
# Bundle app source
COPY simpleapp.py /src/simpleapp.py
COPY index.html  /src/templates/index.html

EXPOSE  8000
CMD ["python", "/src/simpleapp.py", "-p 8000"]

