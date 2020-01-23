FROM mcr.microsoft.com/dotnet/core/aspnet:3.0-buster-slim AS base

RUN apt update
RUN apt install -y libgdiplus
RUN ln -s /usr/lib/libgdiplus.so /lib/x86_64-linux-gnu/libgdiplus.so
RUN apt-get install -y --no-install-recommends zlib1g fontconfig libfreetype6 libx11-6 libxext6 libxrender1 wget gdebi
RUN wget https://github.com/wkhtmltopdf/wkhtmltopdf/releases/download/0.12.5/wkhtmltox_0.12.5-1.stretch_amd64.deb
RUN gdebi --n wkhtmltox_0.12.5-1.stretch_amd64.deb

RUN apt install libssl1.0
RUN ln -s /usr/local/lib/libwkhtmltox.so /usr/lib/libwkhtmltox.so

# https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.xenial_amd64.deb # Ubuntu 16.04 (xenial)
# https://downloads.wkhtmltopdf.org/0.12/0.12.5/wkhtmltox_0.12.5-1.bionic_amd64.deb # Ubuntu 18.04 (bionic)
#libjpeg-turbo8

WORKDIR /app
EXPOSE 80
EXPOSE 443


# Download libwkhtmltox and install it's dependencies
#RUN apt-get update \
    #&& apt-get install -y --no-install-recommends \
        #zlib1g \
        #fontconfig \
        #libfreetype6 \
        #libx11-6 \
        #libxext6 \
        #libxrender1 \
		#libgdiplus \
    #&& curl -o /usr/lib/libwkhtmltox.so \
        #--location \
        #https://github.com/rdvojmoc/DinkToPdf/raw/v1.0.8/v0.12.4/64%20bit/libwkhtmltox.so
#


FROM mcr.microsoft.com/dotnet/core/sdk:3.0-buster AS build
WORKDIR /src
COPY ["Messer.Services.Pdf/Messer.Services.Pdf.csproj", "Messer.Services.Pdf/"]
RUN dotnet restore "Messer.Services.Pdf/Messer.Services.Pdf.csproj"
COPY . .
WORKDIR "/src/Messer.Services.Pdf"
RUN dotnet build "Messer.Services.Pdf.csproj" -c Release -o /app

FROM build AS publish
RUN dotnet publish "Messer.Services.Pdf.csproj" -c Release -o /app

FROM base AS final


WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "Messer.Services.Pdf.dll"]
