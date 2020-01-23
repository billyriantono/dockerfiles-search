FROM evarga/jenkins-slave

RUN apt-get -q update
RUN DEBIAN_FRONTEND="noninteractive" apt-get -q -y -o Dpkg::Options::="--force-confnew" --no-install-recommends upgrade

RUN apt-get -q install -y git unzip

# Add SSH configuration
RUN mkdir /home/jenkins/.ssh
ADD known_hosts /home/jenkins/.ssh/
RUN chown -R jenkins /home/jenkins/.ssh

