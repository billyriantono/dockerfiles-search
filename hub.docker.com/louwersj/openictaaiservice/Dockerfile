FROM louwersj/ol7-pyai-rest

MAINTAINER Johan Louwers Capgemini version: 0.1

# as part of the RUN we will pull code from the
# public github and ensure we move all required 
# code components to the right location. In our
# case we will move all application code to the 
# default location /myprojectenv and we have to 
# make sure we aquire the openIctaAiService code
# and place it at that (/myprojectenv) location.
# additional remark is that you need to ensure 
# that runappcore.sh has execution rights.
RUN yum -y install git &&\
git clone https://github.com/OracleLinuxWorld/inControlTicketAi /tmp/codedrop &&\
mv -v /tmp/codedrop/openICTA/openIctaAiService/appcore/* /myprojectenv &&\
chmod +x /myprojectenv/runappcore.sh &&\
rm -r /tmp/codedrop/ &&\
yum clean all &&\
rm -rf /var/cache/yum/* &&\
rm -rf /var/tmp/*



# Exposing port 8000 which is the port we will be 
# used by gunicorn to run the flask based core
# application. Advised is not to change the default 
# 8000 port unless you are sure about what you are 
# doing. 
EXPOSE 8000

# start the appcore by running the logic in runappcore.sh
# any changes you need in the startup should be made to 
# the runappcore.sh script while keeping the below CMD
# command as it is at the moment. 
CMD ["/myprojectenv/runappcore.sh"]
