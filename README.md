# JSON Schema Relationships - Links Vs Properties

### Links

For this schema, each object's relationships are defined as an object under a "links" property. Each property of that object is the name of the relationship, and the value is  a single object with the "type" and "id" of the related object. For "to-many" relationships, the value can be an array of the same objects.

```javascript
var data = {
  "articles": [{
    "id": "article1",
    "links": {
      "author": {"id": "person1", "type": "people"}
    }
  }],
  "people": [{
    "id": "person1",
    "phoneNumber": "1234"
  }]
};

function getLink(data, object, linkName) {
  var link = object.links[linkName];
  if (link && data[link.type]) {
    return data[link.type].find(function(e) {return e.id === link.type;});
  }
}

getLink(data, data.articles[0], 'author').phoneNumber; // "1234"
```
