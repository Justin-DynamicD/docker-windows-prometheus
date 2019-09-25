###
# start builder
###

# set default args
ARG VERSIONNANO=1809
ARG VERSIONALERTMANAGER=0.19.0

# builder is running core, as nano does not support msi nor gui-dependant exe installers
FROM mcr.microsoft.com/windows/servercore:${VERSIONNANO} as builder
ARG VERSIONALERTMANAGER
ENV VERSIONALERTMANAGER $VERSIONALERTMANAGER

# Download and extract
ADD https://github.com/prometheus/alertmanager/releases/download/v$VERSIONALERTMANAGER/alertmanager-$VERSIONALERTMANAGER.windows-amd64.tar.gz c:/install/alertmanager.tar.gz
RUN cd c:\install && tar -xvf alertmanager.tar.gz
RUN powershell "Get-ChildItem C:\install -Filter alertmanager-* -directory | Rename-Item -NewName alertmanager"

###
# start nano container
###

FROM mcr.microsoft.com/windows/nanoserver:${VERSIONNANO}

# Copy from builder and configure
COPY --from=builder C:/install/alertmanager C:/alertmanager

# bootstrap jenkins at startup
CMD c:\alertmanager\alertmanager.exe --config.file=c:\alertmanager\alertmanager.yml

# LABEL and EXPOSE to document runtime settings
EXPOSE 9093/tcp
LABEL maintainer="justin.dynamicd@gmail.com"
LABEL description="AlertManager for Windows"