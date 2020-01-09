# Use an official Python runtime as a parent image
FROM python:3.5-slim

# Copy the current directory contents into the container at /vagrant
COPY . /wechat_bot

# Set the working directory to /app
WORKDIR /wechat_bot/wechat_bot_proj

# Install any needed packages specified in requirements.txt
RUN apt-get update && apt-get install -y xdg-utils sqlite3 libsqlite3-dev \
                                        mysql-server git fontconfig \
                                        ttf-wqy-microhei ttf-wqy-zenhei nginx\
                                        nginx gcc g++ default-libmysqlclient-dev --fix-missing
RUN pip install --upgrade pip &&  pip install --trusted-host pypi.python.org --no-cache-dir -r ../pip_dependency
# install supervisord that suport python3.X
RUN pip install git+https://github.com/Supervisor/supervisor@master
RUN pip install git+https://github.com/swmt172/ItChat.git
# Make port 80 available to the world outside this container
EXPOSE  8001
EXPOSE  443
# Define environment variable
ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

# Run app.py when the container launches
#CMD ["circusd", "ustarbox_circus.ini"]