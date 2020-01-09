# https://github.com/tiangolo/uvicorn-gunicorn-fastapi-docker
FROM tiangolo/uvicorn-gunicorn-fastapi:python3.7

# create app directory
RUN mkdir -p /deploy
WORKDIR /deploy

# install dependencies
RUN pip install aiofiles
RUN pip install fastapi
RUN pip install imgurpython
RUN pip install jinja2
RUN pip install praw
RUN pip install uvicorn
RUN pip install git+https://github.com/ankeshanand/py-gfycat

# get app source
COPY . /deploy/

# Expose necessary ports and start the server
EXPOSE 80
CMD [ "uvicorn", "app:app", "--host", "0.0.0.0", "--port", "80"]
