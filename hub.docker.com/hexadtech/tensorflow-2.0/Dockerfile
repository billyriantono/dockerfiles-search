FROM python:3.7

RUN python -V
# Check Python version
RUN python -c 'import sys; sys.exit(sys.version_info.major != 3)'
# We need Python runtime environment to execute Python functions.
RUN wget https://s3-us-west-2.amazonaws.com/ntnxsherlock-runtimes/python-env.tgz
RUN tar xf /python-env.tgz
# Bundle does not come with all required packages but defines them as PIP dependencies
COPY requirements.txt ./
RUN pip install -r ./requirements.txt

# Copy pre-trained weights to the container
COPY data /data

# Containers should NOT run as root as a good practice
# We mandate all runtime containers to run as user 10001
USER 10001
# Finally run Python function worker which pull and executes functions.
CMD ["/python-env/run.sh"]
