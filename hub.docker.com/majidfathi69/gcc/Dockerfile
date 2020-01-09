FROM gcc:latest 
COPY . /usr/src/myapp 
WORKDIR /usr/src/myapp 
RUN gcc  -lstdc++ -o myapp main.cpp
CMD ["./myapp"]
