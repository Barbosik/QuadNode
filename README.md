# quad-node

![npm package](https://nodei.co/npm/quad-node.png?downloads=true&downloadRank=true&stars=true)
<br />
<br />
![Language](https://img.shields.io/badge/language-node.js-yellow.svg)
![License](https://img.shields.io/badge/license-APACHE2-blue.svg)

Simple and fast Quad Tree implementation written in node.js

## Install
```
npm install quad-node
```

Also, you can found the latest stable package here: https://www.npmjs.com/package/quad-node


## Usage

### Add reference:
```
var QuadNode = require('quad-node');
```

### Create QuadTree (4 childs per level, max 10 levels)
```
var quadTree = new QuadNode({ minx: -100, miny: -100, maxx: 100, maxy: 100 }, 4, 10);
```

### Insert item
```
var item0 = {
	bound: { minx: 0, miny: 0, maxx: 10, maxy: 10 },
	id: 0
};
quadTree.insert(item0);
```


### Search
```
var bound = { minx: 5, miny: 5, maxx: 8, maxy: 8 };
quadTree.find(bound, function(item) {
	console.log("Found item id="+item.id);
});
```

### Check if any item exists in specified bounds
```
var bound = { minx: 5, miny: 5, maxx: 8, maxy: 8 };
if (quadTree.any(bound)) {
    console.log("specified boundary contains at least one item");
}
```

### Check if any item exists in specified bounds with item filter
```
var bound = { minx: 5, miny: 5, maxx: 8, maxy: 8 };
if (quadTree.any(bound, function(item) { return item.id==0; })) {
    console.log("specified boundary contains at least one item with id==0");
}
```


### Update item
```
item0.bound = { minx: 20, miny: 20, maxx: 25, maxy: 25 };
quadTree.update(item0);
```

### Remove item
```
quadTree.remove(item0);
```

### Clear all
```
quadTree.clear();
```

### Get quad tree statistics (for debuggig purposes)
```
console.log("Total nodes in the quad tree: " + quadTree.scanNodeCount());
console.log("Total items in the quad tree: " + quadTree.scanItemCount());
```

## Remarks

* field "bound" for the item is mandatory and should be present. It's used by QuadNode to determine item boundaries.
* QuadNode will assign field "_quadNode" to the item. This field is reserved for internal QuadNode usage and should not be modified from user code.
* item should belong to single QuadNode and should not be inserted twice. 
