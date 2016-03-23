A generic java implementation of a Distributed Hash Table.
This implementation uses the [OpenKad](http://code.google.com/p/openkad/) Key Based Routing library as an infrastructure.

## DHT Usage Example ##
```
// getting an instance and creating
Injector injector = Guice.createInjector(
    new KadNetModule()
        .setProperty("openkad.net.udp.port", "5555"),
						
    new SimpleDHTModule()
);
			
KeybasedRouting kbr = injector.getInstance(KeybasedRouting.class);
kbr.create();

// create a storage		
DHTStorage storage = injector.getInstance(AgeLimitedDHTStorage.class)
    .create();

// create the dht and register the storage class			
DHT dht = injector.getInstance(DHT.class)
    .setName("dht")
    .setStorage(storage)
    .create();

// join the network
// format of the uri: [protocol]://[address:port]/
kbr.join(new URI("openkad.udp://1.2.3.4:5555/"));



// put some data into the dht
dht.put("any arbitrary data 1", "tag1", "tag2");
dht.put("any arbitrary data 2", "tag3");
dht.put("any arbitrary data 3", "tag3");

// get the data back
List<Serializable> vals = dht.get("tag1", "tag2");
System.out.println(vals); // should print ["any arbitrary data 1"]

vals = dht.get("tag3");
System.out.println(vals); // should print ["any arbitrary data 2", "any arbitrary data 3"]

```




## E-Wolf Project ##
  * [openkad](http://code.google.com/p/openkad/)
  * [dht](http://code.google.com/p/dht/)
  * [chunkeeper](http://code.google.com/p/chunkeeper/)
  * [social-fs](http://code.google.com/p/social-fs/)
  * [ewolf](http://code.google.com/p/ewolf/)
  * [postman](https://code.google.com/p/postman-pubsub/)