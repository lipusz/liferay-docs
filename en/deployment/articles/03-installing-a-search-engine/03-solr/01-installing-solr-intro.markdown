---
header-id: installing-solr
---

# Installing Solr

[TOC levels=1-4]

Solr is a popular enterprise search platform built on Apache Lucene. It's
reliable, scalable, and fault tolerant. Read more about it
[here](http://lucene.apache.org/solr/).

[Elasticsearch](/docs/7-2/deploy/-/knowledge_base/d/configuring-the-liferay-elasticsearch-connector)
is the default search engine that ships with @product@, and some Liferay Search
features are only available on Elasticsearch. It's valid, however, to use Solr
instead. In particular, if you've already been using Solr with a previous
version of @product@, or your platform (for example, your OS or JVM) 
[isn't supported by Elasticsearch](https://www.elastic.co/support/matrix), you might
choose to use Solr to search and index your @product@ data.

There are circumstances that force you to use Elasticsearch instead of Solr.
Read
[here](/docs/7-2/deploy/-/knowledge_base/d/installing-a-search-engine#choosing-a-search-engine)
for more information.

Liferay DXP 7.2, Fix Pack 1 and later, supports Solr 7.5.x through the Liferay
Connector to Solr 7 application.

Liferay Portal CE 7.2, GA2 and later (not available at time of writing), support
Solr 7.5.x through the Liferay CE Connector to Solr 7 application.

## Blacklisting Elasticsearch-Only Features

Before installing Solr, you must 
[blacklist](/docs/7-2/user/-/knowledge_base/u/blacklisting-osgi-bundles-and-components) 
certain DXP 
[features that only work with Elasticsearch](/docs/7-2/deploy/-/knowledge_base/d/installing-a-search-engine#choosing-a-search-engine). 

1.  Create a configuration file named

    ```sh
    com.liferay.portal.bundle.blacklist.internal.BundleBlacklistConfiguration.config
    ```

2.  Give it these contents:

    ```properties
    blacklistBundleSymbolicNames=["com.liferay.portal.search.tuning.web.api","com.liferay.portal.search.tuning.web","com.liferay.portal.search.tuning.synonyms.web","com.liferay.portal.search.tuning.rankings.web"]
    ```

3. Place the file in `Liferay Home/osgi/configs`. 

It is required during the Solr installation process to also 
[stop the Elasticsearch Connectors](https://portal.liferay.dev/docs/7-2/deploy/-/knowledge_base/d/installing-solr-basic-installation#stopping-the-elasticsearch-connector) 
that ship with @product@. If you're ready to blacklist those bundles now, use
these contents in the blacklist configuration file:

```properties
    blacklistBundleSymbolicNames=["com.liferay.portal.search.tuning.web.api","com.liferay.portal.search.tuning.web","com.liferay.portal.search.tuning.synonyms.web","com.liferay.portal.search.tuning.rankings.web","com.liferay.portal.search.elasticsearch6.api","com.liferay.portal.search.elasticsearch6.impl","Liferay Connector to X-Pack Monitoring [Elastic Stack 6.x]","Liferay Connector to X-Pack Security [Elastic Stack 6.x]"]
```

Community Edition users can exclude the X-Pack bundles, as they are DXP-only
bundles.
