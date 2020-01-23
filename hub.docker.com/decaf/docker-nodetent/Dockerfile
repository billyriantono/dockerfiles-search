FROM microsoft/dotnet-framework:4.7.1-windowsservercore-1709

ENV USER_IIS_MANAGER iis-manager
ENV USER_IIS_PASSWORD Password01!

SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

#download Roslyn nupkg and ngen the compiler binaries
RUN Invoke-WebRequest https://api.nuget.org/packages/microsoft.net.compilers.2.3.1.nupkg -OutFile c:\microsoft.net.compilers.2.3.1.zip ; \
    Expand-Archive -Path c:\microsoft.net.compilers.2.3.1.zip -DestinationPath c:\RoslynCompilers ; \
    Remove-Item c:\microsoft.net.compilers.2.3.1.zip -Force ; \
    &C:\Windows\Microsoft.NET\Framework64\v4.0.30319\ngen.exe install c:\RoslynCompilers\tools\csc.exe /ExeConfig:c:\RoslynCompilers\tools\csc.exe | \
    &C:\Windows\Microsoft.NET\Framework64\v4.0.30319\ngen.exe install c:\RoslynCompilers\tools\vbc.exe /ExeConfig:c:\RoslynCompilers\tools\vbc.exe  | \
    &C:\Windows\Microsoft.NET\Framework64\v4.0.30319\ngen.exe install c:\RoslynCompilers\tools\VBCSCompiler.exe /ExeConfig:c:\RoslynCompilers\tools\VBCSCompiler.exe | \
    &C:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe install c:\RoslynCompilers\tools\csc.exe /ExeConfig:c:\RoslynCompilers\tools\csc.exe | \
    &C:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe install c:\RoslynCompilers\tools\vbc.exe /ExeConfig:c:\RoslynCompilers\tools\vbc.exe | \
    &C:\Windows\Microsoft.NET\Framework\v4.0.30319\ngen.exe install c:\RoslynCompilers\tools\VBCSCompiler.exe  /ExeConfig:c:\RoslynCompilers\tools\VBCSCompiler.exe ;

ENV ROSLYN_COMPILER_LOCATION c:\\RoslynCompilers\\tools

RUN Add-WindowsFeature Web-Server; \
    Add-WindowsFeature Web-Windows-Auth; \
    Add-WindowsFeature Web-Stat-Compression; \
    Add-WindowsFeature Web-Dyn-Compression; \	 
    Add-WindowsFeature NET-Framework-45-ASPNET; \
    Add-WindowsFeature Web-Asp-Net45; \
    Add-WindowsFeature NET-WCF-TCP-Activation45; \ 
    Add-WindowsFeature NET-WCF-HTTP-Activation45; \
    Add-WindowsFeature Web-WebSockets; \
    Add-WindowsFeature Web-Mgmt-Service; \
    Add-WindowsFeature Web-ISAPI-Ext; \
    Add-WindowsFeature Web-ISAPI-Filter; \
    Add-WindowsFeature Web-Basic-Auth; \
    Invoke-WebRequest -Uri  https://dotnetbinaries.blob.core.windows.net/servicemonitor/2.0.1.1/ServiceMonitor.exe -OutFile C:\ServiceMonitor.exe
	
RUN New-ItemProperty -Path HKLM:\SOFTWARE\Microsoft\WebManagement\Server -Name EnableRemoteManagement -Value 1 -Force; \
    Set-Service -name WMSVC -StartupType Automatic;

ENTRYPOINT ["C:\\ServiceMonitor.exe", "w3svc"]

RUN NET USER $Env:USER_IIS_MANAGER $Env:USER_IIS_PASSWORD /ADD ; \
    NET LOCALGROUP "Administrators" $Env:USER_IIS_MANAGER /ADD ;

RUN windows\system32\inetsrv\appcmd.exe set config 'Default Web Site/' -section:system.webServer/security/authentication/windowsAuthentication /enabled:"True" /commit:apphost ; \
    windows\system32\inetsrv\appcmd.exe set app 'Default Web Site/' /enabledProtocols:"http,net.tcp" /commit:apphost ;

EXPOSE 80
EXPOSE 8172
