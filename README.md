# fluentd-elasticsearch

This repo contains a Dockerfile for a fluentd container with an elasticsearch output

## Example how to use with Docker
This example assumes that you have an elasticsearch server running on localhost on port 9200
Create a simple config file:

```
<source>
  @type http
  port 8000
  bind 0.0.0.0
  format json
</source>
<match **>
  @type elasticsearch
  host localhost
  port 9200
  index_name kukta
  type_name bar_type
</match>
```


```docker run --net=host -d -p 8000:8000 -v `pwd`:/fluentd/etc -e FLUENTD_CONF=fluentd.conf szaharici/fluentd-elasticsearch```

To test:
```
curl -XPOST -d '{"blah":"blah"}' localhost:8000
```
