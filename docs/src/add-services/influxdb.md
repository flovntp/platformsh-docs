---
title: "InfluxDB (Database service)"
weight: 3
description: |
  InfluxDB is a time series database optimized for high-write-volume use cases such as logs, sensor data, and real-time analytics.
sidebarTitle: "InfluxDB"
---

{{% description %}}

It exposes an HTTP API for client interaction. See the [InfluxDB documentation](https://docs.influxdata.com/influxdb) for more information.

## Supported versions

| Grid | {{% names/dedicated-gen-3 %}} | {{% names/dedicated-gen-2 %}} |
|------|-------------------------------|------------------------------ |
|  {{< image-versions image="influxdb" status="supported" environment="grid" >}} | {{< image-versions image="influxdb" status="supported" environment="dedicated-gen-3" >}} | {{< image-versions image="influxdb" status="supported" environment="dedicated-gen-2" >}} |

{{% image-versions-legacy "influxdb" %}}

## Relationship

The format exposed in the ``$PLATFORM_RELATIONSHIPS`` [environment variable](../development/variables/use-variables.md#use-platformsh-provided-variables):

{{< relationship "influxdb" >}}

## Usage example

{{% endpoint-description type="influxdb" /%}}

{{< codetabs >}}

---
title=PHP
file=static/files/fetch/examples/php/influxdb
highlight=php
---

<--->

---
title=Node.js
file=static/files/fetch/examples/nodejs/influxdb
highlight=js
---

{{< /codetabs >}}

## Exporting data

To export your data from InfluxDB, follow these steps:

1. Install and set up the [`influx` CLI](https://docs.influxdata.com/influxdb/cloud/tools/influx-cli/).
2. Connect to your InfluxDB service with the [Platform.sh CLI](../administration/cli/_index.md):

   ```bash
   platform tunnel:open --host {{<variable "RELATIONSHIP_NAME" >}}
   ```

	That command opens an SSH tunnel to all services on your current environment and produces output like:

   ```bash
   SSH tunnel opened to influxtimedb at: http://admin:<HASH>@127.0.0.1:30000
   ```
3. Retrieve the username and password for your service with `platform tunnel:info`.
4. Generate an [API token](https://docs.influxdata.com/influxdb/cloud/security/tokens/create-token/).
5. Run InfluxDB's CLI backup command and [adapt it as desired](https://docs.influxdata.com/influxdb/v2.3/reference/cli/influx/backup/).

   ```bash
	influx backup {{<variable "BACKUP_DIRECTORY" >}} --host http://127.0.0.1:30000
   ```
