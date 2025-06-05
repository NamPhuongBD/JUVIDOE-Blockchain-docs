# Enable Prometheus metrics

### Overview

EVMBuilder Edge can report and serve the Prometheus metrics, which in their turn can be consumed using Prometheus collector(s).

Prometheus metrics are disabled by default. It can be enabled by specifying the listener address using `--prometheus` flag or `Telemetry.prometheus` field in the config file. Metrics will be served under `/metrics` on the specified address.

### Available metrics

The following metrics are available:

| **Name**                                       | **Type** | **Description**                             |
| ---------------------------------------------- | -------- | ------------------------------------------- |
| txpool\_pending\_transactions                  | Gauge    | Number of pending transactions in TxPool    |
| consensus\_validators                          | Gauge    | Number of Validators                        |
| consensus\_rounds                              | Gauge    | Number of Rounds                            |
| consensus\_num\_txs                            | Gauge    | Number of Transactions in the latest block  |
| consensus\_block\_interval                     | Gauge    | Time between this and last block in seconds |
| network\_peers                                 | Gauge    | Number of Connected peers                   |
| network\_outbound\_connections\_count          | Gauge    | Number of outbound connections              |
| network\_inbound\_connections\_count           | Gauge    | Number of inbound connections               |
| network\_pending\_outbound\_connections\_count | Gauge    | Number of pending outbound connections      |
| network\_pending\_inbound\_connections\_count  | Gauge    | Number of pending inbound connections       |
