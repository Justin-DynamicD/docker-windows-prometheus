###
# start builder
###

# set default args
ARG VERSIONNANO=1809
ARG VERSIONPROMETHEUS=2.12.0

# builder is running core, as nano does not support msi nor gui-dependant exe installers
FROM mcr.microsoft.com/windows/servercore:${VERSIONNANO} as builder
ARG VERSIONPROMETHEUS
ENV VERSIONPROMETHEUS $VERSIONPROMETHEUS

# Download and extract
ADD https://github.com/prometheus/prometheus/releases/download/v$VERSIONPROMETHEUS/prometheus-$VERSIONPROMETHEUS.windows-amd64.tar.gz C:/install/prometheus.tar.gz
RUN cd c:\install && tar -xvf prometheus.tar.gz
RUN powershell "Get-ChildItem C:\install -Filter prometheus-* -directory | Rename-Item -NewName prometheus"

###
# start nano container
###

FROM mcr.microsoft.com/windows/nanoserver:${VERSIONNANO}

# Copy from builder and configure
COPY --from=builder C:/install/prometheus C:/prometheus

# bootstrap jenkins at startup
CMD c:\prometheus\prometheus.exe --config.file=c:\prometheus\prometheus.yml

# LABEL and EXPOSE to document runtime settings
EXPOSE 9090/tcp
LABEL maintainer="justin.dynamicd@gmail.com"
LABEL description="Prometheus for Windows"