FROM microsoft/aspnetcore:2
RUN apt-get update 
RUN apt-get install libgdiplus -y
RUN ln -s /usr/lib/libgdiplus.so.0 /usr/lib/gdiplus.dll
