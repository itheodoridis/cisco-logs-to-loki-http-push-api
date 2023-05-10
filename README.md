# Project Readme

## What this repo is about

This is meant to provide a quick reference to my blog post in [https://www.mythryll.com/]

The Blog post shows how to setup a log server stack for Cisco Network Devices logs, so that it's possible to tag and filter logs by host ip address, severity/priority/facility and then to be able to search by text in those. Finally the Grafana Ecosystem allows for more ways then one to expand the capabilities of such a solution with alerting, using APIs to query logs, etc.

This repo shows how to forward the logs to loki with http using Promtai's Push API, avoiding use of local storage in the docker host, while logs are also processed by Promtail to extract fields and turn them into labels.

It is a modification of the project contained in [https://github.com/itheodoridis/cisco-logs-to-loki-local-storage/]. The idea for that project to export the Cisco logs to file storage using a template belongs to Peter Czanik, the creator of Syslog-ng who has blogged about this here:
[https://www.syslog-ng.com/community/b/blog/posts/parsing-cisco-logs-in-syslog-ng]

I took this idea and moved it further so that the logs are processed by Promtail, labels are detected and exchanged or preserved and then the logs are forwarded to Loki, in order to be displayed in Grafana. A separate repo will be built with the necessary files and settings for extracting the logs and forwarding them directly to Loki using http and the Promtail push API. More about that in my blog post.

A docker-compose.yml file is provided along with a basic file and folder infrastructure to get the stack going on Docker.

The software versions used to create this were the following:

- Grafana v.9.5.1
- Loki 2.8.1
- Promtail 2.8.0
- Syslog-ng 3.38

## What you need to do besides cloning this

- create an ssl directory under the grafana folder, and place the certificate files you need there in order to run Grafana in https. You can easily find a way to generate self-signed certificates or use certs from a private CA if you have that in your organization. If you mean to use this in a publicly facing network then you should use regular certificates from a Public CA but in that case maybe you should reconsider if you really want to use Docker for that (most of the time people advise against its use in production, let alone in public facing systems). Make sure you put the correct filenames for the certs and the hostname for your server (better create also an alias without the domain suffix while you are at it). Those names need to be adjusted in the docker-compose.yml file as well, both in the bind volume entries but also in the enviroment variables.
- start the containers with docker-compose up -d or docker compose up -d if you have a recent edition of docker and docker compose.

## Having trouble?

If you are having trouble then go ahead and create an issue, and I will try and get back to you. I am not a logging expert, far from it. So I will do what I can to help, up to a point.
