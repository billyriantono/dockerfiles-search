FROM node
run npm install -g @oracle/ojet-cli
run ojet create ojectproject --template=navbar:web
workdir /ojectproject
expose 8000
cmd ojet serve