# Use ubuntu base docker image
FROM phusion/baseimage:latest
CMD ["/sbin/my_init"]

# Install python, pip, and c dev libs
RUN apt-get -q update && \
 apt-get install --no-install-recommends -y -q \
   python2.7 python3.4 python2.7-dev python3.4-dev python-pip build-essential git mercurial \
   libffi-dev libssl-dev libxml2-dev \
   libxslt1-dev libpq-dev libmysqlclient-dev libcurl4-openssl-dev \
   libjpeg-dev zlib1g-dev libpng12-dev \
   gfortran libblas-dev liblapack-dev libatlas-dev libquadmath0 \
   libfreetype6-dev pkg-config swig \
   && \
 apt-get clean && rm /var/lib/apt/lists/*_*

# Setup locale
ENV LANG C.UTF-8

# Timezone
ENV TZ=America/New_York
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone

# Upgrade pip and install virtualenv system-wide.
RUN pip install --upgrade pip virtualenv

WORKDIR /app

# Use 8080
EXPOSE 8080
ENV PORT 8080

# The user's Dockerfile must specify an entrypoint with ENTRYPOINT or CMD.
CMD []
