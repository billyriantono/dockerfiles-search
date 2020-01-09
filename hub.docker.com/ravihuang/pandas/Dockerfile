FROM jupyterhub/jupyterhub

MAINTAINER Ravi Huang <ravi.huang@gmail.com>

ARG DEBIAN_FRONTEND=noninteractive

ENV PYTHONUNBUFFERED 1

RUN mkdir -p /opt/pandas/build/
COPY requirements.txt /opt/pandas/build/requirements.txt

COPY import.py /
COPY cli /opt/conda/bin/cli

RUN apt-get update && apt-get install -y --no-install-recommends gnupg2 && \
    gpg2 --keyserver hkp://keys.gnupg.net --recv-keys E19F5F87128899B192B1A2C2AD5F960A256A04AF && \
    echo "deb http://cran.rstudio.com/bin/linux/debian stretch-cran35/">>/etc/apt/sources.list && \
    apt-get install -y --no-install-recommends libatlas-base-dev gfortran pkg-config \
    					              jupyter libfreetype6-dev libpng-dev libx11-dev libzmq3-dev r-base r-base-dev && \
    chmod +x /opt/conda/bin/cli && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
        

# Set default CRAN repo
RUN echo 'options("repos"="http://cran.rstudio.com")' >> /usr/lib/R/etc/Rprofile.site

# Install IRkernel
RUN Rscript -e "install.packages('IRkernel')" -e "IRkernel::installspec()"
    
RUN pip install -r /opt/pandas/build/requirements.txt

EXPOSE 8000

