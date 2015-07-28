js-native-ternary-buffer-tree
=============================

A native Node module implementing a sorted set of Buffers.

The goal is for super-duper-fast string matching. That means inputs and outputs
are always Buffers.

The implementation is a ternary search tree. That strikes a good balance:
memory usage isn't as excessive as with a hash table, and lookups aren't as
slow as with a binary search tree.

Usage
-----

```javascript
var TernaryBufferTree = require('js-native-ternary-buffer-tree');
// Input is a single Buffer: newline-separated Strings.
//
// Performance will be best if the Strings are sorted in UTF-8 byte order.
var tree = new TernaryBufferTree(new Buffer('bar\nbaz\nfoo\nmoo\nthe foo', 'utf-8'));

console.log(tree.contains('foo')); // true
console.log(tree.contains('moo')); // false

console.log(tree.findAllMatches('the foo drove over the moo', 2)); // [ 'the foo', 'foo', 'moo' ]
```

findAllMatches
--------------

This method is interesting in that it can search for tokens that span multiple
words (the second argument specifies the number of words), in a memory-efficient
manner. The memory used is the size of the output Array. The time complexity is
on the order of the size of the input times the number of tokens.

Developing
----------

Download, `npm install`.

Run `mocha -w` in the background as you implement features. Write tests in
`test` and code in `src`.

LICENSE
-------

AGPL-3.0. This project is (c) Overview Services Inc. Please contact us should
you desire a more permissive license.
