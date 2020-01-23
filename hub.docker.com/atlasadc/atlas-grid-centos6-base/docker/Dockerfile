# Get debian with ruby as base image
FROM ruby:latest
MAINTAINER Aaron T. Giovannini <aaron.giovannini@byteheed.com>, https://bitbucket.org/agiovannini/JekyllDeployer

# Update repositories
RUN ["apt-get", "update"]
RUN ["apt-get", "upgrade", "-y"]

# Install jekyll with gem
RUN ["gem", "install", "jekyll", "bundler"]

# Install dependencies
RUN ["apt-get", "install",  "-y", "tree", "apt-utils", \
      "dos2unix", "python3-pip", "nodejs", "python3-yaml" ]

#Install dependencies to our scripts
RUN ["pip3", "install", "addict", "ipython"]


# set tmp for install
WORKDIR /tmp
# Copy our scripts
COPY ./opt /tmp/jekyll_deploy
COPY ./opt/lib/python /usr/lib/python3/dist-packages

RUN mkdir /opt/jekyll_deploy && mv /tmp/jekyll_deploy /opt

#Include in path our binary folder
ENV PATH="/opt/jekyll_deploy/bin:${PATH}"

#Set production enviromen  to Jekyll
ENV JEKYLL_ENV production

# Set our working path to finish deploy
WORKDIR /opt/jekyll_deploy


# In order to prevent that docker could be created in windows will fix windows issues
# Set all bin content executable
RUN ["bash", "-c", "chmod +x /opt/jekyll_deploy/bin/*"]
RUN ["bash", "-c", "dos2unix /opt/jekyll_deploy/bin/*"]


# Set finally image usage path
COPY ./opt/site /www
WORKDIR /www

CMD ["bash", "-c", "echo \"--NOT-COPY-THIS-LINES--\nuse this sample config\nName file as .jekyll.deploy.json\n--START-COPY-NEXT-LINE--\" && cat sample.json"]

# CMD ["deploy_jekyll"]
