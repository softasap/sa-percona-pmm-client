sa-percona-pmm-client
=====================

[![Build Status](https://travis-ci.org/softasap/sa-percona-pmm-client.svg?branch=master)](https://travis-ci.org/softasap/sa-percona-pmm-client)

The PMM platform is based on a simple client-server model that enables efficient scalability. It includes the following modules:

PMM Client is installed on every database host that you want to monitor. It collects server metrics, general system metrics,
 and query analytics data for a complete performance overview. Collected data is sent to PMM Server.

PMM Server is the central part of PMM that aggregates collected data and presents it in the form of tables, dashboards, and graphs in a web interface.

The modules are packaged for easy installation and usage. It is assumed that the user should not need to understand what are the exact tools that make up each module and how they interact. 
However, if you want to leverage the full potential of PMM, internal structure is important.

PMM Client packages consist of the following:

`pmm-admin` is a command-line tool for managing PMM Client, for example, adding and removing database instances that you want to monitor. For more information, see Managing PMM Client.

`percona-qan-agent` is a service that manages the Query Analytics (QAN) agent as it collects query performance data. It also connects with QAN API in PMM Server and sends over collected data.

`node_exporter` is a Prometheus exporter that collects general system metrics. For more information, see https://github.com/prometheus/node_exporter.

`mysqld_exporter` is a Prometheus exporter that collects MySQL server metrics. For more information, see https://github.com/percona/mysqld_exporter.

`mongodb_exporter` is a Prometheus exporter that collects MongoDB server metrics. For more information, see https://github.com/percona/mongodb_exporter.

`proxysql_exporter` is a Prometheus exporter that collects ProxySQL performance metrics. For more information, see https://github.com/percona/proxysql_exporter.

Simple Scenario
If you have just one MySQL or MongoDB server, you can install and run both modules (PMM Client and PMM Server) on this one database host.

Typical Scenario
It is more typical to have several MySQL and MongoDB server instances distributed over different hosts. In this case, you can run PMM Server on a dedicated monitoring host, and install PMM Client on every database host that you want to monitor. Data from hosts will be aggregated on the PMM Server.

![Typical scenario](https://www.percona.com/doc/percona-monitoring-and-management/_images/pmm-diagram.png)

Example of usage (all parameters are optional)

Simple

```YAML
  roles:
    - {
        role: "sa-percona-pmm-client"
      }
```

Advanced:


```YAML

  roles:
    - {
        role: "sa-percona-pmm-client"
      }

```


After you install PMM Client, it does not automatically connect to PMM Server.

To connect the client to PMM Server, specify the IP address using the `pmm-admin config --server` command. 
For example, if PMM Server is running on `192.168.100.1`, and you installed PMM Client on a machine with IP `192.168.200.1`:

```bash
$ sudo pmm-admin config --server 192.168.100.1
OK, PMM server is alive.

PMM Server      | 192.168.100.1
Client Name     | ubuntu-amd64
Client Address  | 192.168.200.1
Note
```

If you changed the default port 80 when running PMM Server, specify it after the servers IP address. For example:

```bash
$ sudo pmm-admin config --server 192.168.100.1:8080
For more information, run pmm-admin config --help.
```


Usage with ansible galaxy workflow
----------------------------------

If you installed the `sa-percona-pmm-client` role using the command


`
   ansible-galaxy install softasap.sa-percona-pmm-client
`

the role will be available in the folder `library/softasap.sa-percona-pmm-client`
Please adjust the path accordingly.

```YAML

     - {
         role: "softasap.sa-percona-pmm-client"
       }

```




Copyright and license
---------------------

Code is dual licensed under the [BSD 3 clause] (https://opensource.org/licenses/BSD-3-Clause) and the [MIT License] (http://opensource.org/licenses/MIT). Choose the one that suits you best.

Subscribe for roles updates at [FB] (https://www.facebook.com/SoftAsap/)
