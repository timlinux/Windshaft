Notes on Caching
-----------------
Consider at least 3 different types of cache:

* Map config and setup (style, interactivity etc). Cache the renderer or Mapnik XML. Invalidation requires knowledge of changes in config or style. (done)
* Serverside caching of generated map tiles cached in LRU or other. Other than simple TTL, Invalidation requires knowledge of changes in map style *or* underlying data.
* Clientside caching by ETag. Requires server to manage ETags per tile and invalidate when style *or* data changes. See serverside caching.

In the case of invalidation caused by data changes, flushing only tiles in the area edited and up their zoom stack is desirable rather than global flush.
Microsoft Quadkeys are a one-dimensional index key that also  encodes properties (zoom level and parent tile) that would aid this style of invalidation. http://msdn.microsoft.com/en-us/library/bb259689.aspx

mini JS LRU cache: https://github.com/rsms/js-lru/blob/master/lru.js or https://github.com/monsur/jscache/blob/master/cache.js.Clear LRU without global puge and maintain access speed. 1 LRU per renderer?