## Task 1 (1/2)

### Clean

- `docker container ls -a`{{execute T1}}

Delete all
- `docker container rm -f $(docker container ls -aq)`{{execute T1}}
- `clear`{{execute T1}}

### Introduction

As we see in the last scenario, a container generate logs on PID 1 in JSON format by default. Docker daemon support more logs type.

EFK suite ( Elasticearch - Fluentd - Kibana) can centralize, process and show logs.

Fluentd is able to process logs with multiple input to multiple output.

The objective is ti centralize all logs in the same place.

### Pratice 

Install Fluentd with docker-compose (which may be similar to a single host docker-orchestrator)

Clone training repo :
- `git clone  https://github.com/Sphinxgaia/training-fluentd.git && cd training-fluentd`{{execute T1}}
- `cp docker-daemon/daemon-katacoda.json /etc/docker/daemon.json`{{execute T1}}
- `systemctl restart docker`{{execute T1}}

Launch EFK stack :
- `docker-compose up -d`{{execute T1}}

Generate httpd Access Logs
- Go to and refresh : https://[[HOST_SUBDOMAIN]]-8081-[[KATACODA_HOST]].environments.katacoda.com/

Confirm Logs from Kibana :
- Go to https://[[HOST_SUBDOMAIN]]-5601-[[KATACODA_HOST]].environments.katacoda.com/
- Then, you need to set up the index name pattern for Kibana. 
  - Please specify fluentd-* to Index name or pattern and press Create button.
  - Then, go to Discover tab to seek for the logs. 
  - As you can see, logs are properly collected into Elasticsearch + Kibana, via Fluentd.


---

> Logs and retention is very important in an ephemeral and elactic environment. Docker has native logs export in a multiple format.
> So you can stream logs from files or export it directly from docker daemon (less storage)