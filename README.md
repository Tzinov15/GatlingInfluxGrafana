# GatlingInfluxGrafana



[![Gatling](./images/gatling.png)](http://gatling.io/#/)

[![InfluxDB](./images/influxdb.png)](https://influxdata.com/)

[![Grafana](./images/grafana.png)](http://grafana.org/)



An easy to follow guide that will help you setup Gatling and visualize the results live with  InfluxDB and Grafana.


[Installation](#prerequisite-installation)  
[Config/Setup](#configuration-and-setup )


# PreRequisite Installation
# Mac OSX (super easy)

InfluxDB:   
`brew install influxdb`

Grafana:  
`brew install grafana/grafana/grafana`

Gatling:  
[Zip Bundle Link]( https://repo1.maven.org/maven2/io/gatling/highcharts/gatling-charts-highcharts-bundle/2.2.2/gatling-charts-highcharts-bundle-2.2.2-bundle.zip)



# Windows (very difficult)

## InfluxDB:
Since InfluxDB does not provide Windows .exe's, the source must be compiled from source from GitHub. This requires installing Go as well as Git

#### Installing Git on Windows

- Get Windows Git Exe from [git-scm.com/downloads](git-scm.com/downloads) and run installer
- Add `git` to the windows path by running `SET %PATH% = %PATH%;C:\Program Files\Git\cmd` from Command Prompt
- Ensure that git and your path are properly setup by running `git --version` from Command Prompt

#### Installing Go in Windows

- Get Windows Go Exe from [https://golang.org/dl/](https://golang.org/dl/) and run installer
- Go should by default be installed directly in `C:\Go` and accordingly update your PATH variable
- If this is not the case, add Go to your path by running `SET %PATH% = %PATH%;C:\Go\bin` and place the Go distribution in `C:\`
- Create a `projects` directory under `C:\Go\` and make sure `GOPATH` is set to `C:\Go\projects`

#### Setting up InfluxDB
Usually the rest should be pretty straight forward. You would run `go get github.com/influxdb/influxdb` to get the latest, run some go install commands, and you would be on your happy way. However, at the time of putting together this Gatling/Influx/Grafana stack, the latest version of master on InfluxDB had a bug with a breaking change in one of its dependencies. I was unable to figure out a clean way to use `go get` and specify a specific branch (and was clearly not the only person who ran into this [issue](http://stackoverflow.com/questions/30188499/how-to-do-go-get-on-a-specific-tag-of-a-github-repository) with Influx), so I came up with a work around. Hold on to your seats:

- Run `go get github.com/influxdb/influxdb`.  
 This will populate your `C:\Go\` directory with some stuff, and more importantly, will populate `C:\Go\projects\src\github.com\influxdata` with a folder called `influxdb`. This folder is an exact copy of the master version of InfluxDB.
- Delete `influxdb` and in its place clone the 0.13 branch of InfluxDB. `git clone -b 0.13 https://github.com/influxdata/influxdb.git` (At the time of writing this .13 was the latest stable version of InfluxDB and it also worked with the version of Grafana that I used)
- Everything else that resulted from `go get github.com/influxdb/influxdb` should be the same with the exception of us swapping the master source code with the .13 branch source code
- Make sure you are inside the the influxdb folder  
 `cd C:\Go\projects\src\github.com\influxdata\influxdb` and run   
  `go get -u -f ./...` and then   
  `go build ./...`

  If all the stars in the universe aligned for you today, then you should have influxdb installed

  The executables should be in `C:\Go\projects\bin\`

  Run `influxd.exe` (or update your PATH to include C:\Go\projects\bin\ and run influxd) and navigate to [http://localhost:8083/](http://localhost:8083/). You should see the InfluxDB Web Interface

## Gatling
[Zip Bundle Link]( https://repo1.maven.org/maven2/io/gatling/highcharts/gatling-charts-highcharts-bundle/2.2.2/gatling-charts-highcharts-bundle-2.2.2-bundle.zip)

- Copy the gatling-charts-highcharts-bundle-2.2.2 folder directly under your C drive (`C:\gatling-charts-highcharts-bundle`)

- Set `GATLING_HOME` to `C:\gatling-charts-highcharts-bundle-2.2.2`
- Update your Path `set PATH=%PATH%;%GATLING_HOME%\bin`

## Grafana

Download the Windows zip containing the exe from [Grafana](http://docs.grafana.org/installation/windows/) and run the installer



# Configuration and Setup
