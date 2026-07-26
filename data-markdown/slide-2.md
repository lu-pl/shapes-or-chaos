**Understanding SHACL** <!-- .element: style="font-size:75px; margin-bottom:1.5em;" -->

<ul>
  <li class="fragment">Focus Nodes</li>
  <li class="fragment">Value Nodes</li>
  <li class="fragment">Constraint Components</li>
</ul>

+++

<div style="text-align:center;">
  <img src="./data-markdown/pics/focus_nodes.png" >
</div>

+++

**SHACL Target Declarations** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" -->


<table style="font-size: 0.7em;">
  <thead>
    <tr>
      <th>Predicate</th>
      <th>Description</th>
    </tr>
  </thead>
  <tbody>
    <tr><td><code>sh:targetNode</code></td><td>Directly point to a node</td></tr>
    <tr><td><code>sh:targetClass</code></td><td>All nodes that are instances of some class</td></tr>
    <tr><td><code>sh:targetSubjectsOf</code></td><td>All nodes that are subjects of some predicate</td></tr>
    <tr><td><code>sh:targetObjectsOf</code></td><td>All nodes that are objects of some predicate</td></tr>
    <tr><td></td><td></td></tr>
  </tbody>
</table>

+++

<div style="ext-align:center;">
  <img src="./data-markdown/pics/value_nodes.png" >
</div>

+++

**Constraint Components** <!-- .element: style="font-size:75px; margin-bottom:1.5em;" --> <br>

<div class="fragment" style="font-size: 0.6em">A <b>Constraint Component</b> is a validation algorithm known to the SHACL engine. <br><b>Constraint Component Parameters</b> invoke and configure a given Constraint Component.</div>

<br>

<div class="fragment" style="font-size: 0.6em">
  <code>sh:datatype</code> → <code>sh:DatatypeConstraintComponent</code>
</div>

+++


```ttl

  ex:PersonShape
	  a sh:NodeShape ;
	  sh:targetClass ex:Person ;
	  sh:property [
		sh:path ex:worksFor ;
		sh:class ex:Company ;
		sh:nodeKind sh:IRI ;
	  ] .
          
```