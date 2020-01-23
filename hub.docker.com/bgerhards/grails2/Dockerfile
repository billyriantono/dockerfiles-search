# start from a Codenvy JDK7 image with Tomcat 7 pre-installed

FROM codenvy/jdk7_tomcat7

# download and install Grails

RUN wget -q -P /home/user http://dist.springframework.org.s3.amazonaws.com/release/GRAILS/grails-2.4.4.zip && \
cd /home/user && unzip grails-2.4.4.zip && rm -rf grails-2.4.4.zip

# set env variables and write them to .bashrc

ENV GRAILS_HOME /home/user/grails-2.4.4
RUN echo “export GRAILS_HOME=$GRAILS_HOME” >> /home/user/.bashrc
ENV PATH $GRAILS_HOME/bin:$PATH
RUN echo “export PATH=$PATH” >> /home/user/.bashrc