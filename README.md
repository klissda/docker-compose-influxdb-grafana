# docker-compose-influxdb-grafana for K6 load testing result

This project is a fork from @jkehres and add a Grafana dashboard to display [K6](https://k6.io/) load testing result

You can run k6 with --out influxdb and point influxdb endpoint to exposed port and db as below,

`k6 run --vus 100 --duration 5m --out influxdb=http://localhost:8086/db0 script.js`

You need to stick with InfluxDB v1 because upstream K6 not support InfluxDB v2 yet. 

# docker-compose-influxdb-grafana

Multi-container Docker app built from the following services:

* [InfluxDB](https://github.com/influxdata/influxdb) - time series database
* [Grafana](https://github.com/grafana/grafana) - visualization UI for InfluxDB

## Quick Start

To start the app:

1. Install [docker-compose](https://docs.docker.com/compose/install/) on the docker host.
1. Clone this repo on the docker host.
1. Optionally, change default credentials or Grafana provisioning.
1. Run the following command from the root of the cloned repo:
```
docker-compose up -d
```

To stop the app:

1. Run the following command from the root of the cloned repo:
```
docker-compose down
```

## Ports

The services in the app run on the following ports:

| Host Port | Service |
| - | - |
| 3000 | Grafana |
| 8086 | InfluxDB |

## Volumes

The app creates the following named volumes (one for each service) so data is not lost when the app is stopped:

* influxdb-storage
* grafana-storage

## Users

The app creates two admin users - one for InfluxDB and one for Grafana. By default, the username and password of both accounts is `admin`. To override the default credentials, set the following environment variables before starting the app:

* `INFLUXDB_USERNAME`
* `INFLUXDB_PASSWORD`
* `GRAFANA_USERNAME`
* `GRAFANA_PASSWORD`

## Database

The app creates a default InfluxDB database called `db0`.

## Data Sources

The app creates a Grafana data source called `InfluxDB` that's connected to the default IndfluxDB database (e.g. `db0`).

To provision additional data sources, see the Grafana [documentation](http://docs.grafana.org/administration/provisioning/#datasources) and add a config file to `./grafana-provisioning/datasources/` before starting the app.

## Dashboards

By default, the app does create [K6 Load Testing Result Grafana dashboard](https://grafana.com/grafana/dashboards/2587). 

To provision additional dashboards, see the Grafana [documentation](http://docs.grafana.org/administration/provisioning/#dashboards) and add a config file to `./grafana-provisioning/dashboards/` before starting the app.
