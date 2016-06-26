# Vera Prometheus exporter

This is a plugin for [Vera][1] controllers which adds a [Prometheus][2] metrics
exporter.

[1]: http://getvera.com/
[2]: https://prometheus.io/

## Exported metrics

Currently gauge metrics are exported for temperature, humidity and light
sensors.

## Installation

Upload all of the `.xml` and `.lua` files in this repository to your Vera
controller.

In UI7, you can do this by navigating to `Apps`, `Develop apps`, `Luup files`
on your controller’s web interface.

Check that the metrics are being properly exported by pointing your browser or
a tool like curl to

```
http://<yourveraip>:49451/data_request?id=lr_prometheus_metrics
```

TODO: Publish this to the mios app store. Please contact me if you are
interested in this plugin and would like me to publish it to the app store.

## Configuration

The metrics are not exposed on the default `/metrics` path that most
Prometheus exporters expose their metrics on, so a little extra configuration
is needed. An example snippet to add to the `scrape_configs` section of your
`prometheus.yml` is:

```yaml
  - job_name: 'vera'
    scrape_interval: 15s
    metrics_path: /data_request?id=lr_prometheus_metrics
    target_groups:
      - targets: ['192.168.8.68:49451']
```

Of course, you should change the IP address in the example (`192.168.8.68`) to
the IP address of your Vera controller.

## License

Licensed under the GPLv3. See the `LICENSE` file for more details.

## Contributing

Pull requests and bug reports welcome!