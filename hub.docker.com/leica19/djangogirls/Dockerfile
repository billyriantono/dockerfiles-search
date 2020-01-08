
FROM leica19/python-ubuntu

# set the working dir to /app
WORKDIR /app

# copy the current dir contents into the container at /app
ADD . .

# install any needed packages in requirements.txt
RUN pip install -r requirements.txt

# make port 80 available to the world outside this container
EXPOSE 8000

CMD ["python", "manage.py", "runserver"]
