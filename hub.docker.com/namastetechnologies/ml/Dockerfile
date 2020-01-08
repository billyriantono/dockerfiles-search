FROM pytorch/pytorch:1.0.1-cuda10.0-cudnn7-runtime

RUN apt-get update && \
    apt-get install -y nginx ca-certificates gcc g++ libc-dev unixodbc-dev  python3-dev python3-venv musl-dev git postgresql python-psycopg2 libpq-dev && \
    apt-get install -y openjdk-8-jdk && \
    apt-get install -y ant && \
    apt-get install ca-certificates-java && \
    update-ca-certificates -f && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

# Setup JAVA_HOME -- useful for docker commandline
ENV JAVA_HOME /usr/lib/jvm/java-8-openjdk-amd64/

ENV PYTHONUNBUFFERED=TRUE
ENV PYTHONDONTWRITEBYTECODE=TRUE

RUN pip install numpy && \
    pip install pandas && \
    pip install scipy && \
    pip install scikit-learn && \
    pip install scikit-surprise==1.0.6 && \
    pip install lightfm==1.15 && \
    pip install h5py==2.9.0 && \
    pip install git+https://github.com/maciejkula/spotlight.git@v0.1.5 && \
    pip install pyspark==2.4.3

# to add a user and start a spark-session
RUN chmod 777 /etc/passwd
