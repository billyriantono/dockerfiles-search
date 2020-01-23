FROM python:3.7-stretch

WORKDIR /tmp

#RUN curl http://ftp.us.debian.org/debian/pool/main/a/apt/apt-transport-https_1.4.9_amd64.deb > apt-transport-https.deb \
#    && dpkg -i apt-transport-https.deb
COPY apt-transport-https_1.4.9_amd64.deb ./
RUN dpkg -i apt-transport-https_1.4.9_amd64.deb

# Install Official Microsoft SQL Server Driver and ODBC
RUN curl https://packages.microsoft.com/keys/microsoft.asc | apt-key add - \
    && curl https://packages.microsoft.com/config/debian/9/prod.list > /etc/apt/sources.list.d/mssql-release.list \
    && apt-get update \
    && ACCEPT_EULA=Y apt-get install -y \
    unixodbc-dev \
    apt-transport-https \
    msodbcsql17 \
    vim \
    && rm -rf /var/lib/apt/lists/*

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt

WORKDIR /usr/app

COPY main.py ./

CMD [ "python", "./main.py" ]
