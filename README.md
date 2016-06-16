# QuadNode
Fast and easy Quad Tree implementation for node.js

## Usage

var QuadNode = require('./QuadNode.js');


// create QuadTree (4 childs per level, max 10 levels)
var quadTree = new QuadNode({ minx: -100, miny: -100, maxx: 100, maxy: 100 }, 4, 10);


// insert item
var item0 = {
	bound: { minx: 0, miny: 0, maxx: 10, maxy: 10 },
	id: 0
};
quadTree.insert(item0);


// search
var bound = { minx: 5, miny: 5, maxx: 8, maxy: 8 };
quadTree.find(bound, function(item) {
	console.log("Found item id="+item.id);
});


// update item
item0.bound = { minx: 20, miny: 20, maxx: 25, maxy: 25 };
quadTree.update(item0);


// remove item
quadTree.remove(item0);


// clear
quadTree.clear();


## Remarks

The field bound should be present for the item. It's used by QuadNode to determine item bounds.
QuadNode will assign _quadNode field to the item. This field is reserved for internal QuadNode usage and should not be modified from user code.