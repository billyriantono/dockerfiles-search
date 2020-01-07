FROM python:stretch

COPY requirements.txt ./
RUN pip install --no-cache-dir -r requirements.txt
   
 RUN apt-get update && apt-get install cron -y \
    ssmtp  \
    vim  \
    && rm -rf /var/lib/apt/lists/* \
    # configure ssmtp to read from env so php's mail() function will work out of the box. 
    && sed -ri -e 's/^(mailhub=).*/\1%%SMTP_HUB%%/' -e 's/^#(FromLineOverride)/\1/' /etc/ssmtp/ssmtp.conf

    
# Add crontab file in the cron directory
ADD crontab /opt/cron/crontabs/hello-cron

# Give execution rights on the cron job
RUN chmod 0644 /opt/cron/crontabs/hello-cron

# Apply cron job
RUN crontab /opt/cron/crontabs/hello-cron

# Create folder for jobs
RUN mkdir -p /var/cron-job

# Run the command on container startup
CMD ["cron", "-f"]


