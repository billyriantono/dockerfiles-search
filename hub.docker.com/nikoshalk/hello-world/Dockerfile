#The Docker image to use as the base image 
FROM gcc:4.9

#Copy the files in the current directory from HOST to the given dest directory in the DOCKER
COPY . /docker/src/hello-world

#Set the the working directory.
WORKDIR /docker/src/hello-world

#run the given command
RUN make

#Set the default executable for this executing container.
CMD [ "./a.out" ]