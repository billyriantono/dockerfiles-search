FROM rbss/jenkins-base:2.0.0
MAINTAINER Dan Sabin <dan.sabin@us.redbullmediahouse.com>

RUN apt-get update && apt-get install -y postgresql-client

# Clear all package lists
RUN rm -rf /var/lib/apt/lists/*