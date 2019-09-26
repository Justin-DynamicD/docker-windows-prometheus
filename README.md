# docker-windows-prometheus

[![Build Status](https://dev.azure.com/Justin-DynamicD/GitHubPipelines/_apis/build/status/Justin-DynamicD.docker-windows-prometheus?branchName=master)](https://dev.azure.com/Justin-DynamicD/GitHubPipelines/_build/latest?definitionId=5&branchName=master)

Dockerfile for creating prometheus in Windows container.

## GitHub public:
https://github.com/Justin-DynamicD/docker-windows-prometheus

Note the version is set to match the version of prometheus.  Therefore v2.12.0 equals v.2.12.0 of Prometheus.

## Running Prometheus

Access occurs on port 9090. In addition, all persistent files are stored on `c:\prometheus` on the container. Therefore, the simplest way to launch the container is to port map and volume map the configuration file as below:

```powershell
docker run -d -p 9090:9090 -v C:/config/prometheus.yml:C:/prometheus/prometheus.yml --name dynamicd/winprometheus:v2.12.0
```

This allows you to use a local config file to run Prometheus.
