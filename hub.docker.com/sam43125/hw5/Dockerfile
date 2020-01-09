FROM sam43125/test:v4
COPY ./*.cpp /usr/src/myapp/
COPY ./*.h /usr/src/myapp/
WORKDIR /usr/src/myapp/
RUN g++ -O3 -o myapp *.cpp
CMD ["./myapp"]
