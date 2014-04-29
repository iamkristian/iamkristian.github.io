---
layout: post
title:  "Elastic Search <small>- Hacking the Y-combinator</small>"
date:   2014-03-14 10:32:41
categories: ruby rails elastic_search
---

I've wanted to dive into Elastic search and see what it does for sometime. Mostly to see how it was working with it.

## Search Basics

When you first dive into search, there's a couple of concepts you need to know about.

### Documents

We denormalize our data into documents. Typical use cases for applying a search engine is on heavily normalized data, that needs to be combined into arbitrary queries, that would make ordinary sql statements too slow or complex, thus joining multiple tables, to only return a few columns.

Other usecases could be fulltext search or geospatial data. Documents are represented by JSON, which makes it a delight to work with.

### The index

Documents are stored in an index. The index is what we search in. As the name state, it is fast to lookup documents in it. In Eleastic Search, the index is a [lucene](http://lucene.apache.org) based index. The greater part of the index is typically loaded into memory, but persisted to disc at index time. So it can be reloaded in case of a server failure.

### The schema

The document structure of the index is defined by a schema. In Elastic Search the schema is dynamic, so it's possible to virtually throw anything at it.

In other lucene based search engines i.e. [Solr](http://solr.apache.org), the schema is static and singular to the server instance. This means the server will have to be reloaded in order for a schema change to take place, and only one index is served. This clearly has its disadvantages.

Te have some structure to the index, we provide a mappings. Which basically define the data types our document should consist of.

Here I've listed an entry for one of the documents.

```json
{
  "_index":"ycombinator",
  "_type":"items",
  "_id":"s6T7pwLNS8y1r4aUQXsoEA",
  "_score":1.0, "_source" : {
    "identifier":"7375376",
    "author":"summerdown2",
    "content":"Very addictive and lots of fun :)",
    "link":"item?id=7375376",
    "points":null,
    "parent":7373566
  }
}
```

### Indexes, Shards, Replica, Nodes, Clusters

Elastic Search operates with multiple indexes. A single index is made of shards, which can be scattered over multiple nodes in a cluster. Each shard can have a replica, which is an exact copy of a shard. This is used to enhance search performance, and as duplication in case of failure.

Indexes support basic create and delete operations on the fly.

## Indexing

So getting data into the search engine is actually a project on its own. Basically there are two ways of populating an index.

- Push data to elastic search, when it is modified
- Query the database for delta changes

The first strategy works nicely if you have a monolithic system of one. If you have multiple sub systems that interact with your data, it would make sense to query the database for deltas.

The indexing task for this project is querying the database, because faults might appear when parsing the ycombinator for data.

Looking at the ``` Item ``` the record boils down to

```ruby
require 'elastic'

class Item < ActiveRecord::Base
  def re_index
    elastic = Elastic.instance
    body = ItemSerializer.new(self).to_json
    elastic.add_item(body)
  end
end
```
The serializer is a simple ``` ActiveModel::Serializer ``` which removes the root element and adds the attributes I want in the index.

```ruby
class ItemSerializer < ActiveModel::Serializer
  self.root = false
  attributes :identifier, :author, :content, :link, :points, :parent
end
```

The interaction with ElasticSearch is wrapped in the ``` Elastic ``` class.

```ruby
require 'elasticsearch'

class Elastic
  include Singleton

  # This creates the index and types at
  # '/name/type/'
  # making the documents available
  def create_index(name, type, body)
    client.index index: name, type: type, body: body
  end

  # Adds documents of type items to the index ycombinator
  def add_item(body)
    create_index('ycombinator', 'items', body)
  end

  # Creates the ElasticSearch client
  def client
    Elasticsearch::Client.new log: true
  end
end
```

## Queries

Finding things again in the index is nicely done using the lucene syntax.

```
Basic syntax
http://localhost:9200/ycombinator/items/_search?q=<query>

Giving query the following:
author:gebe        # Will return documents with author gebe
+author:gebe       # Will make author=gebe mandatory for results
-author:gebe       # Will make exclude author gebe from results
```
Querying throug the gem would add this to the ``` Elastic ``` class

```ruby
def search(options = {})
  client.search(index: 'ycombinator', type: 'items', body: options)
end
```
A search for the string ``` nice ``` in the content would look like this

```ruby
result = es.search( query: { match: { content: 'nice' } } )
```

## Facets

Facets are a way of summerizing on the data in the index. Lets assume I want to find how many items an author have created, I could as the index to facet over authors.

This would change our query to this

```ruby
result = es.search( query: { match: { content: 'nice'}},
            facets: { tags: { terms: { field: 'author' } }} )
```
This actually combines the search result with the facets.

## More

This is far from an exhaustive example of ElasticSearch. More a sort of scratching the surface.

If you want to check out the code I used, you can find it on [Github](http://github.com/iamkristian/elastic-talk)

