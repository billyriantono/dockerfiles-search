FROM microsoft/windowsservercore

RUN powershell Invoke-WebRequest -UseBasicParsing -Uri http://go.microsoft.com/fwlink/?LinkId=691126 -OutFile C:\Users\ContainerAdministrator\Downloads\cpp.exe
RUN start /wait C:\Users\ContainerAdministrator\Downloads\cpp.exe /quiet

CMD ["cmd"]
