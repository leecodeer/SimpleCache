# SimpleCache
A Cache framework for java and android application.
用Java实现的缓存工框架，可用于Java和Android项目开发中的缓存数据，你可以实现Cache和CacheFactoryStrategy来自定义你的缓存实现逻辑。使用HashMap进行存储，键为String，值可以为任意对象类型，如String,List,Map等。

# how to use

  	Cache<String, Object> objectCache = CacheFactory.createCache("objects");
        //set max cache size
        objectCache.setMaxCacheSize(1024 * 1024);
        //set max lifetime for cache objects
        objectCache.setMaxLifetime(60 * 60 * 1000);

        objectCache.put("object1", new Object());
        objectCache.put("object2", new Object());
        objectCache.put("object3", new Object());

        Object o1 = objectCache.get("object1");
        if(o1 == null){
            //get data from file or datebase
        }
        //get cache hits
        long cacheHits = objectCache.getCacheHits();
        //get cache miss
        long cacheMiss = objectCache.getCacheMisses();
        //remove cache
        Object o2 = objectCache.remove("object1");
        if(o2 != null) {o2 = null;}

        //you can also use Collection as cache value
        
        Cache<String, Collection<String>> collectionCache = CacheFactory.createCache("collections");
        collectionCache.put("collection1", Arrays.asList("hello", "simple cache"));
        //you can get lock for this collection
        Lock lock = CacheFactory.getLock("collection1", collectionCache);
        lock.lock();
        //do something
        lock.unlock();
        
        //delete cache
        CacheFactory.destroyCache("object1");
        CacheFactory.destroyCache("collection1");
