![elasticsearch logo](http://i.imgur.com/xl1xgjm.png)


In the next 30 mins you will learn how to use ElasticSearch
to power a great search experience for your project/product/website.

## Why?

For anything more than a basic website, ***people expect*** to be
able to ***search*** through your content (blog posts, recipes, products, reviews, etc.)

You *could* use [**google custom search**](https://www.google.com/cse) to
provide this functionality and side-step having to run your own cluster
of search servers...  But I suspect your project/customer wants/needs more
control over the search experience and that's why you're reading this...

## Why *Not* XYZ Database (that *has* Full-Text-Search) ?

Simple/Short answer: Pick the ***Best tool for the job***.

In the past I've used MongoDB's full-text-search (and even wrote a
  [tutorial](https://github.com/ideaq/mongo-search) for it!) I've used
  [MySQL full-text-search](http://dev.mysql.com/doc/refman/5.0/en/fulltext-search.html)
  to *reasonable* success (Deal Searcher V.1 @Groupon!) and many of my
  *Rails* friends swear by
  [Postgres full-text-search](http://www.postgresql.org/docs/8.3/static/textsearch.html)
  but none of these databases were *designed from scratch* to provide
  *scalable* full-text search. So, if you want search, ***elasticsearch***!

## What?

Elasticsearch is a search server based on
[Lucene](http://en.wikipedia.org/wiki/Lucene).
It provides a distributed, multitenant-capable **full-text search** engine
with a RESTful web interface and schema-free JSON documents.
i.e. *awesomeness in a box*!

> Read more: http://www.elasticsearch.org/overview/elasticsearch/


## How?

> http://www.elasticsearch.org/blog/client-for-node-js-and-the-browser
> http://www.elasticsearch.org/guide/en/elasticsearch/client/javascript-api/current/quick-start.html


### Download & Install

Given that ElasticSearch ***requires Java 7***, I've created a Vagrant box
to consistently boot ES on any OS (using a VM!)

#### Vagrant + Ubuntu

If you aren't using Vagrant, go read my vagrant tutorial *now*:
https://github.com/nelsonic/learn-vagrant

- Install ElasticSearch on Ubuntu:
https://www.digitalocean.com/community/tutorials/how-to-install-elasticsearch-on-an-ubuntu-vps


#### Mac

```sh
brew install elasticsearch
```

To have launchd start elasticsearch at login:
```
ln -sfv /usr/local/opt/elasticsearch/*.plist ~/Library/LaunchAgents
```
Then to load elasticsearch now:
```
launchctl load ~/Library/LaunchAgents/homebrew.mxcl.elasticsearch.plist
```
Or, if you don't want/need launchctl, you can just run:
```
elasticsearch --config=/usr/local/opt/elasticsearch/config/elasticsearch.yml
```

- http://stackoverflow.com/questions/22850247/installing-elasticsearch-on-osx-mavericks

#### Running ElasticSearch on *Any* OS with Vagrant

If you are unfamiliar with vagrant please take a few minutes
to read: https://github.com/nelsonic/learn-vagrant



- http://www.elasticsearch.org/overview/elkdownloads/

```sh
curl -XPUT 'http://localhost:9200/twitter/tweet/1' -d '{"user":"kimchy","post_date":"2009-11-15T14:12:12","message" : "trying out Elasticsearch"}'
```


### Install (Node Module)

```sh
npm install elasticsearch --save
```


## ElasticSearch Server Status

```
curl -XGET http://localhost:9200
```
see: http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/indices-status.html


# > Continue:

- [ ] http://www.sitepoint.com/building-recipe-search-site-angular-elasticsearch/  
- [x] http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_conventions_used_in_this_book.html  
- [ ] http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_talking_to_elasticsearch.html
- [ ] http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/_talking_to_elasticsearch.html
- [ ] Video: http://www.elasticsearch.org/webinars/getting-started-with-elasticsearch/?watch=1

### Video Tutorial Code:

If you want to follow along with the ElasticSearch getting started video:

Insert a record:
```sh
curl -XPUT 'http://localhost:9200/vehicles/tv/one' -d '{"color":"green","driver":{"born":"1959-09-07","name":"Walter White"},"make":"Pontiac","model":"Aztek","value_usd":5000.0, "year":2003}'
```

Check the **mapping** for the index:
```sh
curl http://localhost:9200/vehicles/_mapping?pretty
```

To delete an index you accidentally created:
```sh
curl -XDELETE 'http://localhost:9200/vehicles/'
```
Search:
```js
curl 'localhost:9200/vehicles/tv/_search?q=_id:one&pretty'
```
Insert another document/record:
```sh
curl -XPUT 'http://localhost:9200/vehicles/tv/two' -d '{"color":"black","driver":{"born":"1949-01-09","name":"Michael Knight"},"make":"Pontiac","model":"Trans Am","value_usd":9999999.00, "year":1982}'
```

curl 'http://localhost:9200/vehicles/_search?q=pontiac&pretty'

### Updating a Record (Index)

The Update API is quite well documented:
http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/docs-update.html



## Useful Links

- Guide: http://www.elasticsearch.org/guide/ (online docs)
- http://www.elasticsearch.org/blog/client-for-node-js-and-the-browser/
- http://thomasardal.com/running-elasticsearch-on-linux-using-vagrant/
- http://www.elasticsearch.org/guide/en/elasticsearch/reference/current/setup-repositories.html
- http://exploringelasticsearch.com/overview.html
- The ***Definitive Guide***: http://www.elasticsearch.org/guide/en/elasticsearch/guide/current/

### Video

- Elasticsearch from the bottom up: https://www.youtube.com/watch?v=PpX7J-G2PEo
- Getting started video:
~~http://www.elasticsearch.org/webinars/getting-started-with-elasticsearch/?watch=1~~
https://www.youtube.com/watch?v=7FLXjgB0PQI (Clinton Gormley)
- Running ES in Travis-CI (build testing): http://docs.travis-ci.com/user/database-setup/#ElasticSearce

## Background Reading

- Elasticsearch (wiki): http://en.wikipedia.org/wiki/Elasticsearch
- Faceted Search: http://en.wikipedia.org/wiki/Faceted_search
- Solr vs Elasticsearch: http://stackoverflow.com/questions/10213009/solr-vs-elasticsearch
- More detailed Solr vs ES: http://blog.sematext.com/2012/08/23/solr-vs-elasticsearch-part-1-overview
- A Clustered Setup: http://mookid.dk/oncode/archives/3518
- Reverse Port Forwarding: http://stackoverflow.com/questions/16244601/vagrant-reverse-port-forwarding/17012410#17012410
- How HipChat use ElasticSearch for storing messages: https://blog.hipchat.com/category/how-hipchat-works/
- Decent (but old) tutorial: http://www.sitepoint.com/building-recipe-search-site-angular-elasticsearch
- **Testing ElasticSearch with Node.js**:
http://faiq.me/testing-elasticsearch-node (use sinon)

### ELK

ELK is a Logging Stack comprised of ElasticSearch, LogStash & Kibana

- http://www.elasticsearch.org/overview/elkdownloads/
- http://www.elasticsearch.org/overview/kibana/
- http://www.elasticsearch.org/overview/logstash/
- https://www.digitalocean.com/community/tutorials/how-to-use-logstash-and-kibana-to-centralize-and-visualize-logs-on-ubuntu-14-04
- Flume: http://flume.apache.org/
- Fluentd: http://www.fluentd.org/


## History

I chose elasticsearch to power the search for a project I lead at [News](http://news.co.uk/)
after careful consideration of Solr.
There are great [heroku addons](https://addons.heroku.com/?q=elasticsearch)
(we used [Bonsai](https://addons.heroku.com/bonsai) because they have
a *free* dev tier) and the quality of the search results is superb.


## Troubleshooting

Tried to start elastic search with:
```
elasticsearch --config=/usr/local/opt/elasticsearch/config/elasticsearch.yml
```
But got the error:
```
Exception in thread "main" java.lang.UnsupportedClassVersionError: org/elasticsearch/bootstrap/Elasticsearch : Unsupported major.minor version 51.0
```


Tried `npm start` but got:

```sh
 npm start

> learn-elasticsearch@0.0.1 start /Users/n/code/learn-elasticsearch
> node index.js

Elasticsearch ERROR: 2014-10-06T20:57:07Z
  Error: Request error, retrying -- getaddrinfo ENOTFOUND
      at Log.error (/Users/n/code/learn-elasticsearch/node_modules/elasticsearch/src/lib/log.js:213:60)
      at checkRespForFailure (/Users/n/code/learn-elasticsearch/node_modules/elasticsearch/src/lib/transport.js:194:18)
      at HttpConnector.<anonymous> (/Users/n/code/learn-elasticsearch/node_modules/elasticsearch/src/lib/connectors/http.js:146:7)
      at ClientRequest.bound (/Users/n/code/learn-elasticsearch/node_modules/elasticsearch/node_modules/lodash-node/modern/internals/baseBind.js:56:17)
      at ClientRequest.emit (events.js:95:17)
      at Socket.socketErrorListener (http.js:1551:9)
      at Socket.emit (events.js:95:17)
      at net.js:833:16
      at process._tickCallback (node.js:419:13)

Elasticsearch WARNING: 2014-10-06T20:57:07Z
  Unable to revive connection: http://elasticsearch1:9200/

Elasticsearch WARNING: 2014-10-06T20:57:07Z
  No living connections
```

> Make sure you put the IP address of your server in your configuration.
