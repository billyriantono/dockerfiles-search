FROM ubuntu:14.04
MAINTAINER Adrian CITU

RUN apt-get update && apt-get install -y python-pip sqlite3 lib32z1-dev python-dev libxml2-dev libxslt-dev libffi-dev libssl-dev
RUN pip install https://github.com/mitsuhiko/flask/tarball/master
RUN pip install owasp-skf

WORKDIR /usr/local/lib/python2.7/dist-packages/skf/ 

#by default the application starts on 127.0.0.1 only
#so must be started in saas mode to be accessible 
#outside of the container. 
ENTRYPOINT ["python" ,"skf.py", "__saas"]



