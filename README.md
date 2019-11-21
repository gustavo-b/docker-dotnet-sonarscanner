# .Net Core Sonar Scanner on Docker Container

Sonar Scanner MsBuild Dockerfile for .Net Core Projects

[![Docker Pulls](https://img.shields.io/docker/pulls/gustavobatista/docker-dotnet-sonarscanner.svg)](https://hub.docker.com/r/gustavobatista/docker-dotnet-sonarscanner/) [![Docker Automated build](https://img.shields.io/docker/automated/gustavobatista/docker-dotnet-sonarscanner.svg)](https://hub.docker.com/r/gustavobatista/docker-dotnet-sonarscanner/) [![Docker Build Status](https://img.shields.io/docker/build/gustavobatista/docker-dotnet-sonarscanner.svg)](https://hub.docker.com/r/gustavobatista/docker-dotnet-sonarscanner/)

## Image Dependencies

|                | Name          | Version       |
| -------------- |:-------------:| -------------:|
| OS             | Debian        |   Stretch (9) |
| Java           | OpenJDK       |  8 Update 171 |
| .NET Framework | Mono          |    5.12.0.226 |
| .NET SDK       | .NET Core SDK |           2.2 |
| Sonar Scanner  | CLI           |    3.2.0.1227 |
| Sonar Scanner  | MS Build      |   4.8.0.12008 |

Please check [Releases Page](https://github.com/burakince/docker-dotnet-sonarscanner/releases) for details.

## Latest Versions

[Latest Debian](https://www.debian.org/releases/stable/)
[Latest OpenJDK](https://hub.docker.com/r/library/openjdk/tags/)
[Latest Mono](https://www.mono-project.com/download/stable/#download-lin-debian)
[Latest .Net SDK](https://www.microsoft.com/net/download/all)
[Latest Sonar Scanner](https://docs.sonarqube.org/display/SCAN/Analyzing+with+SonarQube+Scanner+for+MSBuild)

## Using Example

First of all you need a SonarQube server, or a project on [SonarCloud](https://sonarcloud.io/). If you don't have one, run this code:

```
docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube
```

And then you need a .Net Core project. If you don't have one, run this code:

```
mkdir ConsoleApplication1
cd ConsoleApplication1

dotnet new console
dotnet new sln
dotnet sln ConsoleApplication1.sln add ConsoleApplication1.csproj
```

Get a login token from your SonarQube server or SonarCloud project, and run this code in the project directory that you wish to analyze:

```
docker run --name dotnet-scanner -it --rm -v $(pwd):/project \
  -e PROJECT_ORGANIZATION=default
  -e PROJECT_KEY=ConsoleApplication1 \
  -e PROJECT_NAME=ConsoleApplication1 \
  -e PROJECT_VERSION=1.0 \
  -e HOST=https://sonarcloud.io \
  -e LOGIN_KEY=CHANGE_THIS_ONE \
  gustavobatista/docker-dotnet-sonarscanner
```

Note: If you have SonarQube as docker container, you must inspect SonarQube's bridge network IP address and use it in HOST variable.

```
docker network inspect bridge
```
