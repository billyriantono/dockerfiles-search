FROM python:3
ENV PYTHONUNBUFFERED 1
# add a new code directory
RUN mkdir /code
# set the directory to the working directory
WORKDIR /code
# put the requirements file in the code directory
COPY requirements.txt /code/
# install the requirements from the file
RUN pip install -r requirements.txt
# copy the rest of the files into the directory
COPY . /code/
