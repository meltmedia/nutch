# Nutch 1.x with ElasticSearch 0.20.5 Client

This is meltmedia's fork of Apache Nutch to support our internal search efforts.

## Building this project

Nutch uses ant to build.  Clone the repository and run `ant`.

## Crawling a Site

Nutch is a little difficult to get running at first.  Here are the basic instructions for performing 
a crawl and getting the crawl data up on elasticsearch.

### Getting started

There is all kinds of voodoo required to get Nutch configured.  I have started the process of adding a configuration
to this repository for crawling a locally mounted afp volume.  After building, change your directory to `runtime/afp` to use this
use this configuration.  [See the readme](https://github.com/meltmedia/nutch/tree/meltmedia-search-1.x/runtime/afp) in that directory for more instructions.

### Perform the Crawl

To perform a crawl, you feed Nutch some seed URLs from a file and then it will populate a local crawl database.  To get
started, echo the URL into the seed file

```
mkdir urls
echo 'URL' >> urls/seed.txt
```
then start the crawler
```
./bin/nutch crawl urls -dir crawl -depth 10 -topN 5
```

### Send the data to Elasticsearch

Once the crawl is complete, feed the data into Elasticsearch using the ElasticsearchIndexer:
```
./bin/nutch org.apache.nutch.indexer.elasticsearch.ElasticsearchIndexer ELASTICSEARCH_DOMAIN 9300 crawl/crawldb crawl/linkdb crawl/segments/*
```
