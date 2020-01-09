FROM ubuntu:16.04

LABEL author="Kersten Breuer, Zeller Team, EMBL 2017" \
    maintainer="kersten-breuer@outlook.com"

# Install essential unix packages and dependencies:
RUN apt-get update -y --fix-missing
RUN apt-get install -y build-essential \
    wget \
    python-dev \
    python3

# copy ena_downloader.py script into the image:
COPY ./ena_raw_downloader.py /usr/local/bin/
# make the script executable:
RUN chmod a+x /usr/local/bin/ena_raw_downloader.py

CMD ["ena_raw_downloader.py"]