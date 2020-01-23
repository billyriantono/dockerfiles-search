FROM ubuntu
RUN apt-get update
RUN apt-get -y install python
COPY ubuntu_docker_msg.py /ubuntu_docker_msg.py
CMD ["python","/ubuntu_docker_msg.py"]
