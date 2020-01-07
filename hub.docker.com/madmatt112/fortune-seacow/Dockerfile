FROM docker/whalesay:latest
RUN apt-get -y update && apt-get install -y fortune
ADD ./scripts /var/lib/jenkins
ADD ./scripts /home/ec2-user/workspace/Fortune-Seacow
CMD seacow.sh