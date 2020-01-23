from ubuntu
label maintainer all-images@devops.com
arg image_vaiable="local"
env ora_port=1521
env ora_host="localhost"
run mkdir /code
copy sample.sh /code/sample.sh
run chmod +x /code/sample.sh
run echo "Building an Image.."
run echo "setting vairiable"
workdir /code
cmd sh /code/sample.sh
