# Pull base image.
FROM ubuntu

# Define working directory.
RUN mkdir /data -p && mkdir /apps -p
WORKDIR /apps
   
ENV STAR_VERSION=2.5.4a
  
RUN apt-get update && apt-get install -y wget 
 
RUN wget https://github.com/alexdobin/STAR/archive/${STAR_VERSION}.tar.gz &&\
  tar xvzf ${STAR_VERSION}.tar.gz


WORKDIR /data


# Define commonly used JAVA_HOME variable
ENV PATH="/apps/STAR-${STAR_VERSION}/bin/Linux_x86_64_static:${PATH}"

# VOLUME /data
# Define default command.
CMD ["STAR"]
