FROM ubuntu

# Update aptitude with new repo
RUN apt-get update

# Install software 
RUN apt-get install -y git
# Make ssh dir
RUN mkdir /root/.ssh/

# Copy over private key, and set permissions
ADD id_rsa /root/.ssh/id_rsa
RUN chmod 400 /root/.ssh/id_rsa

# Create known_hosts
RUN touch /root/.ssh/known_hosts
# Add bitbuckets key
RUN ssh-keyscan bitbucket.org >> /root/.ssh/known_hosts
RUN ssh -T git@bitbucket.org

RUN mkdir -p /var/www/html/docroot
#VOLUME /var/www/html/docroot

# Clone the conf files into the docker container
RUN yes | git clone git@bitbucket.org:alexsoftteam/user_service.git /var/www/html/docroot
