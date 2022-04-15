### Create backup from influx
```bash
influxd backup -portable -database mydatabase {-host <remote-node-IP>:8088} {-start 2022-01-12T16:09:52.563635Z} /tmp/mysnapshot
influxd backup -portable -database mydatabase -start 2022-01-12T16:09:52.563635Z .
```

### Query for timeseries
```
SELECT mean(first_metric), max(second_metric) FROM your_measurement WHERE time > 1642247031s and time < 1644838967s group by time(15m) fill(0) limit 5;
```

### filter by tag and field
```
SELECT * from ipsla_loss where fieldname='key' and tagname='key' limit 1;
```

### query for tag keys on measurement
```
show tag values from "measurement" with key = "tag_name"
```

### query for tag values on measurement with tag key
```
show tag values from "measurement" with key = "tag_name" where "tag_name" =~ /.+some_text.+/
```

