# Start from base Python 3.7 flask image
FROM stephenneal/python-flask:3.7-slim
LABEL maintainer="Stephen Neal <stephen@stephenneal.net>"

ENV aws_access_key_id=""
ENV aws_secret_access_key=""
ENV aws_region_name=""

# Expose port 5000
EXPOSE 5000

# Set working directory
WORKDIR /var/www

# Copy app config and uWSGI runner
COPY ["wsgi.py", "app.ini", "logging.conf", "entrypoint.sh", "aws-credentials.sh", "/var/www/"]

# Copy source code
COPY MarketingImg /var/www/MarketingImg
COPY setup.py /var/www/setup.py
RUN pip3 install --upgrade pip && pip3 install -e /var/www

# Run app at the conclusion of build
CMD ./entrypoint.sh