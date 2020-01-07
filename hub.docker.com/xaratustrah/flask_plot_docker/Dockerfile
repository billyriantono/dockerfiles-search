FROM python:3.6.4

# Create the group and user to be used in this container
RUN groupadd flaskgroup && useradd -m -g flaskgroup -s /bin/bash flask

# Create the working directory (and set it as the working directory)
RUN mkdir -p /home/flask/app/flask_plot
WORKDIR /home/flask/app/flask_plot

# Install the package dependencies (this step is separated
# from copying all the source code to avoid having to
# re-install all python packages defined in requirements.txt
# whenever any source code change is made)

COPY requirements.txt /home/flask/app/flask_plot
RUN pip install --no-cache-dir -r requirements.txt


# Copy the source code into the container
COPY . /home/flask/app/flask_plot

RUN chown -R flask:flaskgroup /home/flask

USER flask

WORKDIR /home/flask/app/flask_plot

CMD [ "/usr/local/bin/gunicorn", "-w", "2", "-b", "0.0.0.0:5000", "flask_plot:app" ]
