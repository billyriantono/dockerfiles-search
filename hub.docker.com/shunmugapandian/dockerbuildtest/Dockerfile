from ubuntu
label maintainer shun@gmail.com
run mkdir /code
copy Sample.sh /code/Sample.sh
run chmod +x /code/Sample.sh
workdir /code
#cmd executes during bootstrap only
#run executes during docker build
cmd sh /code/Sample.sh
