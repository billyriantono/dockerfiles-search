FROM gcc:latest
LABEL Name=stat__binomial Version=0.0.1 maintainer="Bryan Perez <@bryanperez43>"

WORKDIR /app
COPY    binomial.cpp /app/

# This command compiles your app using GCC, adjust for your source code
RUN g++ -o binomial binomial.cpp

# This command runs your application, comment out this line to compile only
CMD ["./binomial"]


