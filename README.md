# Nutch 1.x with ElasticSearch 0.20.5 Client

This is meltmedia's fork of Apache Nutch to support our internal search efforts.

## Building this project

Nutch uses ant to build.  Clone the repository and run `ant`.

## Crawling a Site

Nutch is a little difficult to get running at first.  Here are the basic instructions for performing 
a crawl and getting the crawl data up on elasticsearch.

### Move into the local runtime directory

After you build Nutch, there will be a newly created directory called `runtime/local` created at the top level 
of the project.  This directory contains an environment for running Nutch.

### Configure Nutch

This is the voodoo part of this process.  Since you will need different configuration for each site you want to crawl, 
I cannot provide you step by step instructions here.

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
