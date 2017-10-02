# Grafana Datasource for DeviceHive 

Currently in development.

This datasource was created to connect Grafana with DeviceHive to track commands and notifications by particular device.

Based on Grafana Simple JSON Datasource plugin.

## Adding the data source to Grafana

Prerequisites: You should have Grafana, npm and yarn installed and have permissions to copy data to Plugins folder(you could set it in `grafana.ini` in `Paths->plugins`).

1. Clone this repo to Plugins folder - `git clone https://github.com/devicehive/devicehive-grafana-datasource.git`;
2. Go into folder - `cd devicehive-grafana-datasource`;
3. Install all packages - `yarn install`;
4. Build plugin - `npm run build`;
5. Restart Grafana - `sudo service grafana-server restart`;
6. Open Grafana in any browser;
7. Open the side menu by clicking the Grafana icon in the top header;
8. In the side menu click `Data Sources`;
9. Click the `+ Add data source` in the top header;
10. Select `DeviceHive` from the `Type` dropdown;
11. Configure datasource.

## Using the data source in Dashboards

1. Open Grafana in any browser;
2. Open the side menu by clicking the Grafana icon in the top header;
3. In the side menu find `Dashboards` and in context menu click `+ New`;
4. Select Panel type from top header. Currently this plugin wirks fine with `Graph` and `Singlestat` types.
5. Click on `Panel Title` and choose `Edit`;
6. In `Metrics` tab choose your data source name from `Panel Data Source`;
7. Choose metric type from dropdown (`command` or `notification`);
8. Type path to variable inside command in input. (Remember you could use object and arrays inside it, f.e. `parameters.testData[0].temperature`);
9. Click time range burron in the top header on the right.
10. Type `now-2m` in `From` text field, choose refreshing option from dropdown and click `Apply`. (Remember cache is available for last 2 minutes only)

## Development

This section is for development purposes only.

General documentation about datasource plugins can be found in the [Docs](https://github.com/grafana/grafana/blob/master/docs/sources/plugins/developing/datasources.md).<br>
There are some prerequisites plugin should have to work with Grafana, you could find them in abovementioned docs.

Response from query should have this kind of shape:

``` javascript
[
  {
    "target":"command", // The field being queried for
    "datapoints":[
      [622,1450754160000],  // Metric value as a float , unixtimestamp in milliseconds
      [365,1450754220000]
    ]
  },
  {
    "target":"notification",
    "datapoints":[
      [861,1450754160000],
      [767,1450754220000]
    ]
  }
]
```