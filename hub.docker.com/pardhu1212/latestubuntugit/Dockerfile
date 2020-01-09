from ubuntu
label maintainer pardhu1212@gmail.com
arg image_variable="local"
run mkdir /code
env ora_port=1521
env ora_host="localhost"
copy Sample.sh /code/Sample.sh
run chmod +x /code/Sample.sh
run echo "Building an image"
run echo $image_variable
workdir /code
cmd sh /code/Sample.sh
