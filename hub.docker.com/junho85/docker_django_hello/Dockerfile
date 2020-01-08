from ubuntu:14.04

maintainer junho85 <junho85@gmail.com>

run apt-get update

run apt-get install -y python3 python3-setuptools
run easy_install3 pip
run pip3 install django

workdir /home/docker/code/
add django_helloworld /home/docker/code/

expose 8000

cmd python3 manage.py runserver 0.0.0.0:8000

