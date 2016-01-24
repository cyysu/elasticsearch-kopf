elasticsearch kopf
=======================

kopf is a simple web administration tool for [ElasticSearch](http://elasticsearch.org) written in JavaScript + AngularJS + jQuery + Twitter bootstrap.

It offers an easy way of performing common tasks on an elasticsearch cluster. Not every single API is covered by this plugin, but it does offer a REST client which allows you to explore the full potential of the ElasticSearch API.

Versions
------------

| elasticsearch version | branch | latest version  |
| --------------------- | ------ | --------------- |
| 0.90.X                | 0.90   | see [master branch README](https://github.com/lmenezes/elasticsearch-kopf/blob/master/README.md) |
| 1.X                   | 1.0    | see [master branch README](https://github.com/lmenezes/elasticsearch-kopf/blob/master/README.md) |
| 2.X                   | 2.0    | see [master branch README](https://github.com/lmenezes/elasticsearch-kopf/blob/master/README.md) |

Installation
------------


####Run locally:

```bash
git clone git://github.com/lmenezes/elasticsearch-kopf.git
cd elasticsearch-kopf
git checkout {version}
open index.html
```

ps: local execution doesn't work with Chrome(and maybe other browsers). See more [here](http://docs.angularjs.org/api/ng.directive:ngInclude).

Alternatively you can run it via `connect` which should solve the `ng-include` issue.

```bash
git clone git://github.com/lmenezes/elasticsearch-kopf.git
cd elasticsearch-kopf
git checkout {version}
npm install
grunt server
```

####Install on a ElasticSearch instance:

```bash
./elasticsearch/bin/plugin --install lmenezes/elasticsearch-kopf/{version}
open http://localhost:9200/_plugin/kopf
```

####Kopf behind a reverse proxy
Example configuration for nginx:
```
server {
  listen       8080;
  server_name  localhost;

  location ~ ^/es.*$ {
    proxy_pass http://localhost:9200;
    rewrite ^/es(.*) /$1 break;
  }

  location ~ ^/kopf/.*$ {
    proxy_pass http://localhost:9200;
    rewrite ^/kopf/(.*) /_plugin/kopf/$1 break;
  }
}
```
Example configuration for kopf(kopf_external_settings.json):
```json
{
  "elasticsearch_root_path": "/es",
  "with_credentials": false,
  "theme": "dark",
  "refresh_rate": 5000
}
```
Access kopf at http://localhost:8080/kopf/
####Try it online:
```
http://lmenezes.com/elasticsearch-kopf/?location=http://localhost:9200
```

####Basic HTTP Auth support:
```
http://lmenezes.com/elasticsearch-kopf/?location=http://user:pwd@localhost:9200
```

if using https://github.com/Asquera/elasticsearch-http-basic, try:
```
http://lmenezes.com/elasticsearch-kopf/?location=http://user:pwd@localhost:9200//
```
The plugin modifies the base elasticsearch response and therefore this workaround is needed.

Screenshots
------------
####cluster overview
![cluster overview](imgs/cluster_view.png)

####header reflects cluster state
![cluster state](imgs/cluster_state.png)

####REST Client
![rest client](imgs/rest_client.png)

####aliases management
![aliases management](imgs/aliases.png)

####warmers management
![warmers management](imgs/warmer.png)

####percolator
![percolator](imgs/percolator.png)

####snapshots management
![snapshots management](imgs/snapshot.png)

####analysis api
![analysis api](imgs/analysis.png)
