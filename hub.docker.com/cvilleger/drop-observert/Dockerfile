FROM python:3.6

# Update package manager to get up to date repositories
RUN pip install --upgrade pip

RUN mkdir /code
ADD . /code/

# used to clone the private dependencies
COPY id_rsa /root/.ssh/id_rsa
COPY known_hosts /root/.ssh/known_hosts
RUN chmod 600 /root/.ssh/id_rsa /root/.ssh/known_hosts

WORKDIR /code
RUN pip install -r requirements.txt
RUN export PYTHONPATH=/code/cleverIntegrator

WORKDIR /code/cleverIntegrator
CMD python application.py