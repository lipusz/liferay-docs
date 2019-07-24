---
header-id: installing-a-search-engine
---

# Installing a Search Engine

[TOC levels=1-4]

A search engine is a critical component of your @product@ installation. If
you're here, you probably know the basics already and want to configure a
search engine for your @product@ deployment. 

Elasticsearch, a highly scalable, full-text search engine, is installed by
default, as an embedded server. Elasticsearch is well-supported and almost
certainly meets any search and indexing need you have, but you must not use the
[embedded version in your production deployment](/docs/7-2/deploy/-/knowledge_base/d/elasticsearch#embedded-vs-remote-operation-mode). 

Learn to configure a remote Elasticsearch server or cluster
[here](/docs/7-2/deploy/-/knowledge_base/d/installing-elasticsearch).

[Solr](http://lucene.apache.org/solr) 
is another capable and popular search engine supported in @product@. 

Learn to configure a remote Solr server or cluster
[here](/docs/7-2/deploy/-/knowledge_base/d/installing-solr). But first, make
sure you understand the disparity in functionality between the supported search
engines.

## Choosing a Search Engine

Elasticsearch and Solr are both supported, but there are limitations to
Liferay's Solr integration. To use any of the following features, you must
choose Elasticsearch. 

End User features:

- [Liferay Commerce](https://help.liferay.com/hc/en-us/articles/360017869952)
- [Workflow Metrics](/docs/7-2/user/-/knowledge_base/u/workflow-metrics-the-service-level-agreement) 
- [Custom Filter search widget (due to lack of support for ComplexQueryPart)](/docs/7-2/user/-/knowledge_base/u/filtering-search-results-with-the-custom-filter-widget)

<!-- Not yet released
- Search Tuning: Result Rankings - Confirming with Dennis
- Search Tuning: Synonyms - Confirming with Dennis-->

Developer Features:

- From Portal Core (Module: `portal-kernel`, Artifact:
    `com.liferay.portal.kernel`):
    -  `com.liferay.portal.kernel.search.generic.NestedQuery`
    -  `com.liferay.portal.kernel.search.filter`:
        -  `ComplexQueryPart`
        -  `GeoBoundingBoxFilter`
        -  `GeoDistanceFilter`
        -  `GeoDistanceRangeFilter`
        -  `GeoPolygonFilter`
- Portal Search API (Module: `portal-search-api`, Artifact:
    `com.liferay.portal.search.api`):
    -  `com.liferay.portal.search.filter`:
        - `ComplexQueryPart`
        - `TermsSetFilter`
    -  `com.liferay.portal.search.geolocation.*`
    -  `com.liferay.portal.search.highlight.*`
    -  `com.liferay.portal.search.query.function.*`
    -  `com.liferay.portal.search.query`:
        -  `BoostingQuery`
        -  `CommonTermsQuery`
        -  `ConstantScoreQuery`
        -  `DateRangeTermQuery`
        -  `ExistsQuery`
        -  `FunctionScoreQuery`
        -  `IdsQuery`
        -  `NestedQuery`
        -  `PercolateQuery`
        -  `PrefixQuery`
        -  `RangeTermQuery`
        -  `RegexQuery`
        -  `ScriptQuery`
        -  `SimpleStringQuery`
    -  `com.liferay.portal.search.script.*`
    -  `com.liferay.portal.search.significance.*`
    -  `com.liferay.portal.search.sort.*`: only `Sort` is supported
- Portal Search Engine Adapter API (Module: `portal-search-engine-adapter-api`,
    Artifact: `com.liferay.portal.search.engine.adapter.api`)
    -  `com.liferay.portal.search.engine.adapter.cluster.*`
    -  `com.liferay.portal.search.engine.adapter.document.UpdateByQueryDocumentRequest`
    -  `com.liferay.portal.search.engine.adapter.index.*`: only
        - `RefreshIndexRequest` is supported
    -  `com.liferay.portal.search.engine.adapter.search.*`: 
        -`MultisearchSearchRequest` 
        - `SuggestSearchRequest`
    -  `com.liferay.portal.search.engine.adapter.snapshot.*`

Liferay Commerce requires the `TermsSetFilter` implementation, only available
in the Elasticsearch connector.

Some of these Elasticsearch-only developer features may be added to the Solr
integration in the future.

Another factor to consider in your search engine selection is JDK version. The
search engine and @product@ must use the same JDK version and distribution
(e.g., Oracle Open JDK 1.8.0_201). Consult the 
[Elasticsearch compatibility matrix](https://www.elastic.co/support/matrix#matrix_jvm) 
and the 
[@product@ compatibility matrix](https://web.liferay.com/documents/14/21598941/Liferay+DXP+7.1+Compatibility+Matrix/9f9c917a-c620-427b-865d-5c4b4a00be85)
to learn more about supported JDK distributions and versions. This consideration
is not necessary for Solr, because no JVM level serialization happens between
the servers. All communication occurs at the HTTP level.

