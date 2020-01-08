FROM gcc:4.9
COPY . /HelloWorld
WORKDIR /HelloWorld
#RUN g++ -o HelloWorld HelloWorld.cpp
RUN make all
CMD ["./HelloWorld"]