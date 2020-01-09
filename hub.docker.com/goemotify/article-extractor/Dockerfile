FROM python:3

# copy all files
COPY . /usr/src/app/

# set working dir path
WORKDIR /usr/src/app

# install dependencies
#RUN cd article_extraction
RUN pip install --no-cache-dir -r requirements.txt

# run app server
CMD ["gunicorn", "src.app"]

# expose container port to machine port
EXPOSE 8000 8000