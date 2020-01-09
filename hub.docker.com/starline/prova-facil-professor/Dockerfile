# Creating image based on official python3 image
FROM python:3

# Sets dumping log messages directly to stream instead of buffering
ENV PYTHONUNBUFFERED 1

WORKDIR /tmp
RUN wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.0.0.1744-linux.zip
RUN unzip sonar-scanner-cli-4.0.0.1744-linux.zip
RUN rm sonar-scanner-cli-4.0.0.1744-linux.zip
RUN mv sonar-scanner-4.0.0.1744-linux/ /opt
RUN mv /opt/sonar-scanner-4.0.0.1744-linux/ /opt/sonar-scanner
ENV PATH="/opt/sonar-scanner/bin:${PATH}"

RUN apt-get update
RUN apt-get install -y apt-transport-https zip gcc

# Creating and putting application inside container
# and setting it to working directory (meaning it is going to be default)
RUN mkdir /src
WORKDIR /src
ADD requirements.txt .

# Installing all python dependencies
RUN pip install -r requirements.txt

# Open port 8000 to outside world
EXPOSE 8000

# When container starts, this script will be executed.
# Note that it is NOT executed during building
#CMD ["sh", "on-container-start.sh"]
