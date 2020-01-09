# Using official python runtime base image
FROM python:3.7.2-stretch
# Environment Variables
ENV AMQP_HOST myaccess
ENV AMQP_PORT mysecret
ENV AMQP_USER myendpoint.de
ENV AMQP_PASS mybucket  
ENV AMQP_RECEIVE_QUEUE mysecret
ENV AMQP_SEND_QUEUE myid

# Set the application directory
WORKDIR /app

# Install our requirements.txt
ADD requirements.txt /app/requirements.txt
RUN CFLAGS="-Wno-narrowing" pip install cld2-cffi
RUN pip install -r requirements.txt

# Copy our code from the current folder to /app inside the container
ADD . /app

RUN pip install textacy[all]
RUN python -m spacy download de
RUN python -m spacy download en


RUN pip install numpy && \
    pip install --upgrade cython && \ 
	pip install -U spacy[cuda92]

	
	
# Define our command to be run when launching the container
#CMD ["python", "app.py"]
