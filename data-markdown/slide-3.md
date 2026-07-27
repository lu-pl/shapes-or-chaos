**SHACL Core** <!-- .element: style="font-size:75px; margin-bottom:1.5em;" --> <br>

+++

**Type Constraints** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>

<br>
<div class="fragment" style="font-size: 0.8em">Type Constraints allow to restrict the type of a given Value Node.</div>

+++

<table style="font-size: 0.7em;">
  <thead>
    <tr>
      <th>Predicate</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>sh:class</code></td><td>Value must be an instance of the given RDFS/OWL class</td></tr>
    <tr><td><code>sh:datatype</code></td><td>Value must be a literal of the given XSD datatype</td></tr>
    <tr><td><code>sh:nodeKind</code></td><td>Value must be an IRI, a blank node, a literal</td></tr>
    <tr><td></td><td></td></tr>
    <tr><td><code>sh:hasValue</code></td><td>The value node must have this specific value</td></tr>
    <tr><td><code>sh:in</code></td><td>Value must be one of an enumerated/fixed list of values</td></tr>
    <tr><td></td><td></td></tr>
  </tbody>
</table>

+++

**Cardinality Constraints** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>

+++

<table style="font-size: 0.7em;">
  <thead>
    <tr>
      <th>Predicate</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>sh:minCount</code></td><td>Minimum number of value nodes required</td></tr>
    <tr><td><code>sh:maxCount</code></td><td>Maximum number of value nodes allowed</td></tr>
  </tbody>
</table>


<br>
<div class="fragment" style="font-size: 0.8em">Note: Default cardinality in SHACL is 0 to unbounded.</div>

+++

<div style="display: flex; text-align: left;">
  <div style="width: 50%;">

```ttl
ex:MinCountExampleShape
	a sh:PropertyShape ;
	sh:targetNode ex:Alice, ex:Bob ;
	sh:path ex:name ;
	sh:minCount 1 .
```
  </div>
  <div style="width: 50%;">

```ttl
ex:Alice ex:name "Alice" .     # pass
ex:Bob ex:givenName "Bob"@en . # fail
```
  </div>
</div>


+++


**Other Cardinality/Range Constraints** <!-- .element: style="font-size:40px; margin-bottom:1em;" --> <br>

<ul>
        <li>sh:minExclusive</li>
        <li>sh:maxExclusive</li>
        <li>sh:minInclusive</li>
        <li>sh:maxInclusive</li>
        <li>sh:minLength</li>
        <li>sh:maxLength</li>
</ul>


+++

**Practical: Type and Cardinality Constraints** <!-- .element: style="font-size:50px; margin-bottom:1.5em;" --> <br>


<ul>
        <li class="fragment"> Go to <a href="https://tinyurl.com/shacl-gist"> https://tinyurl.com/shacl-gist </a> </li>
        <li class="fragment"> Example 2: Follow the link to the SHACL Playground </li>
        <li class="fragment"> Exercise: 🐱‍💻 ✅</li>
</ul>


+++

**Property Pair Constraints** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>

<br>

<div class="fragment" style="font-size: 0.8em">Property pair constraints allow to specify conditions <br>in relation to other properties.</div>

<br>

<div class="fragment" style="font-size: 0.8em;">Property pair constraints compare the <em>Value Nodes</em> <br> of two property paths originating from the same <em>Focus Node</em>.</div>

+++

<table style="font-size: 0.7em;">
  <thead>
    <tr>
      <th>Predicate</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>sh:equals</code></td><td>Value Nodes must be equal</td></tr>
    <tr><td><code>sh:disjoint</code></td><td>Value Nodes must be disjoint</td></tr>
    <tr><td><code>sh:lessThan</code></td><td>A given Value Node must be LT</td></tr>
    <tr><td><code>sh:lessThanOrEquals</code></td><td>A given Value Node must be LE</td></tr>
    <tr><td></td><td></td></tr>
  </tbody>
</table>

+++

<div style="display: flex; text-align: left;">
  <div style="width: 50%;">

```ttl
ex:DisjointExampleShape
	a sh:NodeShape ;
	sh:targetNode ex:USA, ex:Germany ;
	sh:property [
		sh:path ex:prefLabel ;
		sh:disjoint ex:altLabel ;
	] .
```
  </div>
  <div style="width: 50%;">

```ttl
# pass
ex:USA
	ex:prefLabel "USA" ;
	ex:altLabel "United States" . 

# fail
ex:Germany
	ex:prefLabel "Germany" ;
	ex:altLabel "Germany" .       
```
  </div>
</div>

+++

**Logical Constraints** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>


+++

<table style="font-size: 0.7em;">
  <thead>
    <tr>
      <th>Predicate</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>sh:not</code></td><td>Value must NOT conform to the given shape</td></tr>
    <tr><td><code>sh:and</code></td><td>Value must conform to ALL of the given shapes</td></tr>
    <tr><td><code>sh:or</code></td><td>Value must conform to AT LEAST ONE of the given shapes</td></tr>
    <tr><td><code>sh:xone</code></td><td>Value must conform to EXACTLY ONE of the given shapes</td></tr>
  </tbody>
</table>

+++

```
ex:PersonShape
  a sh:NodeShape ;
  sh:targetClass ex:Person ;

  sh:property [
    sh:path ex:gender ;
    sh:maxCount 1 ;
  ] ;

  sh:or (
    [
      sh:path ex:gender ;
      sh:in ( ex:Male ex:Female ex:NonBinary )
    ]
    [
      sh:path ex:gender ;
      sh:datatype xsd:string
    ]
  ) .
```

+++


```ttl
ex:PersonShape
  a sh:NodeShape ;
  sh:targetClass ex:Person ;

  sh:property [
    sh:path ex:gender ;
    sh:maxCount 1 ;
    sh:or (
      [ sh:in ( ex:Male ex:Female ex:NonBinary ex:Other ) ]
      [ sh:datatype xsd:string ]
    )
  ] .
```

+++

**Qualified Value Shapes** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>


<div class="fragment" style="font-size: 0.8em">Qualified Value Shapes allow to define the condition <br>that a specified number of value nodes conforms to a given shape.</div>

+++


```ttl
ex:HandShape a sh:NodeShape ;
	sh:targetClass ex:Hand ;

	sh:property [
  		sh:path ex:digit ;
  		sh:class ex:Thumb ;
  		sh:minCount 1 ;
  		sh:maxCount 1 ;
	] ;
	sh:property [
  		sh:path ex:digit ;
  		sh:class ex:Finger ;
  		sh:minCount 4 ;
  		sh:maxCount 4 ;
	] .
```

+++

```ttl
ex:HandShape a sh:NodeShape ;
	sh:targetClass ex:Hand ;
	sh:property [
		sh:path ex:digit ;
		sh:minCount 5 ;
		sh:maxCount 5 ;
	] ;
	sh:property [
		sh:path ex:digit ;
		sh:qualifiedValueShape [ sh:class ex:Thumb ] ;
		sh:qualifiedValueShapesDisjoint true ;
		sh:qualifiedMinCount 1 ;
		sh:qualifiedMaxCount 1 ;
	] ;
	sh:property [
		sh:path ex:digit ;
		sh:qualifiedValueShape [ sh:class ex:Finger ] ;
		sh:qualifiedValueShapesDisjoint true ;
		sh:qualifiedMinCount 4 ;
		sh:qualifiedMaxCount 4 ;
	] .
```

+++

**Shape-based Constraints** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>

<div class="fragment" style="font-size: 0.8em">Shape-based constraint components can be used to specify complex conditions by validating the value nodes against certain shapes. </div>

+++

<table style="font-size: 0.7em;">
  <thead>
    <tr>
      <th>Predicate</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>sh:qualifiedValueShape</code></td><td>Constrains how many values (of an already-resolved set) must conform to a given shape</td></tr>
    <tr><td><code>sh:property</code></td><td>Navigates via a new path from the current node, then validates the resulting values against a property shape</td></tr>
    <tr><td><code>sh:node</code></td><td>Validates the current value node directly against another shape</td></tr>
  </tbody>
</table>

+++

```ttl
ex:AddressShape
	a sh:NodeShape ;
	sh:property [
		sh:path ex:postalCode ;
		sh:datatype xsd:string ;
		sh:maxCount 1 ;
	] .

ex:PersonShape
	a sh:NodeShape ;
	sh:targetClass ex:Person ;
	sh:property [
		sh:path ex:address ;
		sh:minCount 1 ;
		sh:node ex:AddressShape ;  # Composition! <3
	] .
```