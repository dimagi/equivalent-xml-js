Equivalent XML JS [![Build status](https://secure.travis-ci.org/theozaurus/equivalent-xml-js.png)](http://travis-ci.org/theozaurus/equivalent-xml-js)
========

Equivalent XML JS is designed to ease the process of testing XML output. The work is a port of [equivalent-xml](https://github.com/mbklein/equivalent-xml)

 - Comparing text output is brittle due to the vagaries of serialization.
 - Attribute order doesn't matter.
 - Element order matters sometimes, but not always.
 - Text sometimes needs to be normalized, but CDATA doesn't.

Usage
=====

    > var doc1 = EquivalentXml.xml("<root><foo a='1' b='2'>Hello</foo><bar>World</bar></root>");
    > var doc2 = EquivalentXml.xml("<root><bar>World</bar><foo b='2' a='1'> Hello </foo></root>");
    > EquivalentXml.isEquivalent(doc1,doc2);
    true
    > EquivalentXml.isEquivalent(doc1,doc2, {element_order: true});
    false
    > EquivalentXml.isEquivalent(doc1,doc2, {normalize_whitespace: false});
    false
    
Options
=======

    {element_order: true }
    
  Require elements to be in the same relative position in order to be considered equivalent.

    {normalize_whitespace: false }
    
  Don't normalize whitespace within text nodes; require text nodes to match exactly.

Using with Jasmine
==================

  In your `SpecHelper.js` file add:
  
    beforeEach(function() {
      this.addMatchers(EquivalentXml.jasmine);
    });
    
  Then in your tests you can write
  
     expect(node_1).beEquivalentTo(node_2);
     expect(node_1).not.beEquivalentTo(node_2);
     expect(node_1).beEquivalentTo(node_2,{element_order: true});

Install tools
=============

If you want to test or build the source you will first need to install node and npm:

    $ npm install

Tests
=====

The tests are run with [Mocha](https://mochajs.org/) and [Chai](https://www.chaijs.com/). The command to run them is:

    $ npm test

Or you can check the current status of master using [Travis](https://travis-ci.com/github/dimagi/equivalent-xml-js)

Supported platforms
===================

It has been tested on:

 - Chrome 18
 - Safari 5
 - Firefox 
