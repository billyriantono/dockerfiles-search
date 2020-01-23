FROM jenkins/jenkins:2.151
# Change to root user to install required packages
USER root
RUN apt-get update && apt-get install
RUN apt-get install -y python-pip 
RUN pip install --upgrade selenium 
RUN apt-get install -y python-virtualenv 
RUN apt-get install -y postgresql-common 
RUN apt-get install -y postgresql-server-dev-all 
RUN apt-get install -y libssl-dev
RUN apt-get install -y gettext python-svn
RUN mkdir -p /var/log/django
# Change to the jenkins user for jenkins-specific modifications
USER jenkins
COPY plugins.txt /usr/share/jenkins/ref/
RUN /usr/local/bin/plugins.sh /usr/share/jenkins/ref/plugins.txt
COPY django /var/log/
# Back to root again?!??
USER root
RUN chown jenkins:jenkins /var/log/django
RUN pip install django-jenkins
RUN pip install pylint
RUN ln -sf /usr/lib/python2.7/dist-packages/pysvn/_pysvn_2_7.x86_64-linux-gnu.so /usr/lib/python2.7/dist-packages/pysvn/_pysvn_2_7.so
RUN python -m pip uninstall pip
# switch back to jenkins user.
USER jenkins

