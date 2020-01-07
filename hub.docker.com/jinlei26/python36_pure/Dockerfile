
# Copy right: JinLei "University of Toronto"

# Set a basic image for your image, you are adviced choose images which is certified by docker officially
FROM python:3.6.9-slim-stretch

# Add important info into your image, comparing the "MAINTAINER", I suggest you to use "LABEL"
LABEL maintainer = "JinLei <llei.jin@mail.utoronto.ca>"
LABEL build_date = "2019-7-29"

# Copy essential files from local to docker server
COPY . /python36

# Set your work adress
WORKDIR /python36

# Install tools and packages you want: "pip3", "libglib2.0-0"
# "libglib2.0-0" is used to interprete python
# Using only one "RUN" will help you to optimize image's size as one layer
# Cleaning after installing!!!!!!!!!
RUN apt-get update && apt-get install -y --no-install-recommends \
    libglib2.0-0 \
    && pip3 install --upgrade pip && pip3 install -r requirements.txt \
    && apt-get clean && \rm -rf /var/lib/apt/lists/* 

# You can write like this to run a python file
# Do not forget add a python file into your Dockerfile address!
#ENTRYPOINT [ "python" ]
#CMD [ "./app.py" ] 
