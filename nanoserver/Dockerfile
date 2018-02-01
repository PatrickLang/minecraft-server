# escape=`
FROM openjdk:8u131-jdk-nanoserver

#SHELL ["powershell", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# TODO: Put the next 3 lines in a PR to https://github.com/PowerShell/PowerShell/blob/master/docker/release/nanoserver/Dockerfile
#USER ContainerAdministrator
#CMD ['cmd.exe', '/c setx /m PATH "C:\Program Files\PowerShell;%PATH%"']
#RUN 'Get-ItemProperty -Path c:\\' 
#USER ContainerUser

#SHELL ["pwsh.exe", "-Command", "$ErrorActionPreference = 'Stop'; $ProgressPreference = 'SilentlyContinue';"]

# TODO: remove this line later - it's just asserting that the SHELL statement works as containeruser
#RUN 'Get-ItemProperty -Path c:\\' 

# TODO: Add Python for mcstatus
# TODO: pip install mcstatus

# Note: 'localhost' can bizarrely resolve to external addresses on some networks
# HEALTHCHECK CMD mcstatus 127.0.0.1 ping

# TODO: Create minecraft user

EXPOSE 25565 25575

ADD https://github.com/itzg/rcon-cli/releases/download/1.3/rcon-cli_windows_amd64.exe /tools/rcon-cli.exe
RUN 'cmd /c setx PATH "C:\tools;%PATH%"'

COPY minecraft /minecraft

VOLUME ["C:\\data","C:\\mods","C:\\config","C:\\plugins","C:\\users\\minecraft"]

USER ContainerAdministrator
# Workaround for symlink issues (https://blog.sixeyed.com/docker-volumes-on-windows-the-case-of-the-g-drive/)
CMD ['reg.exe', 'ADD "HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\DOS Devices" /v "G:" /t REG_SZ /d "\??\C:\data"']
#RUN Set-ItemProperty -Path 'HKLM:\SYSTEM\CurrentControlSet\Control\Session Manager\DOS Devices' -Name 'G:' -Value "\??\C:\data" -Type String;  
USER ContainerUser

WORKDIR G:\

ENTRYPOINT [ "pwsh.exe", "-File", "C:\\minecraft\\start.ps1" ]

ENV UID=1000 `
    GID=1000 `
    MOTD="A Minecraft Server Powered by Docker" `
    JVM_XX_OPTS="-XX:+UseG1GC" `
    MEMORY="1G" `
    TYPE=VANILLA`
    VERSION=LATEST `
    FORGEVERSION=RECOMMENDED `
    LEVEL=world `
    PVP=true `
    DIFFICULTY=easy `
    ENABLE_RCON=true `
    RCON_PORT=25575 `
    RCON_PASSWORD=minecraft `
    LEVEL_TYPE=DEFAULT `
    GENERATOR_SETTINGS= `
    WORLD= `
    MODPACK= `
    ONLINE_MODE=TRUE `
    CONSOLE=true