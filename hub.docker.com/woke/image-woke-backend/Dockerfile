FROM python:3.6
LABEL maintainer="dev@woke.xyz"
RUN apt-get update -y
RUN apt-get -y upgrade
RUN apt-get install -y python-pip python-dev build-essential
RUN apt-get install -y virtualenv python-virtualenv
RUN virtualenv virtual-woke-backend
RUN /bin/bash -c "source virtual-woke-backend/bin/activate"
RUN pip3 install appnope==0.1.0
RUN pip3 install Django==2.0.1
RUN pip3 install blinker==1.4
RUN pip3 install cryptography==2.2.2
RUN pip3 install django-browserid==2.0.2
RUN pip3 install django-classy-tags==0.8.0
RUN pip3 install django-rest-framework-mongoengine==3.3.1
RUN pip3 install django-sekizai==0.10.0
RUN pip3 install djangorestframework==3.7.7
RUN pip3 install djangorestframework-jwt==1.11.0
RUN pip3 install idna==2.6
RUN pip3 install ipython==6.2.1
RUN pip3 install ipython-genutils==0.2.0
RUN pip3 install jedi==0.11.1
RUN pip3 install mongoengine==0.15.0
RUN pip3 install nexmo==2.0.0
RUN pip3 install oauthlib==2.0.7
RUN pip3 install parso==0.1.1
RUN pip3 install passlib==1.7.1
RUN pip3 install pexpect==4.4.0
RUN pip3 install pickleshare==0.7.4
RUN pip3 install prompt-toolkit==1.0.15
RUN pip3 install ptyprocess==0.5.2
RUN pip3 install pycparser==2.18
RUN pip3 install Pygments==2.2.0
RUN pip3 install PyJWT==1.6.1
RUN pip3 install pymongo==3.6.1
RUN pip3 install PySocks==1.6.8
RUN pip3 install python-dotenv==0.8.2
RUN pip3 install pytz==2018.3
RUN pip3 install requests==2.18.4
RUN pip3 install requests-oauthlib==0.8.0
RUN pip3 install simplegeneric==0.8.1
RUN pip3 install six==1.11.0
RUN pip3 install traitlets==4.3.2
RUN pip3 install tweepy==3.6.0
RUN pip3 install urllib3==1.22
RUN pip3 install wcwidth==0.1.7
RUN pip3 install django-cors-headers==2.3.0
RUN pip3 install fcm-django
RUN pip3 install unidecode
RUN pip3 freeze > requirements.txt
EXPOSE 8000