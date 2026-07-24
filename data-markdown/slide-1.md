**SHACL Overview** <!-- .element: style="font-size:75px; margin-bottom:1.5em;" --> <br>

- SHACL: Shapes Constraint Language <!-- .element: class="fragment" -->
- W3C Standard and Specification<!-- .element: class="fragment" -->
- Modules: SHACL Core, SHACL-SPARQL, SHACL AF <!-- .element: class="fragment" -->
- SHACL Processors: <!-- .element: class="fragment" -->
  - pySHACL
  - rudof
  - Apache Jena SHACL
  - ... 

+++

Basic SHACL Example
```ttl

  ex:PersonShape
	  a sh:NodeShape ;
	  sh:targetClass ex:Person ;
	  sh:property [
		sh:path ex:ssn ;
		sh:maxCount 1 ;
		sh:datatype xsd:string ;
		sh:pattern "^\\d{3}-\\d{2}-\\d{4}$" ;
	  ] ;
	  sh:property [
		sh:path ex:worksFor ;
		sh:class ex:Company ;
		sh:nodeKind sh:IRI ;
	  ] ;
	  sh:closed true ;
	  sh:ignoredProperties ( rdf:type ) .
          
```


+++

**SHACL Processing** <!-- .element: style="font-size:50px; margin-bottom:1.5em;" --> <br>

<div style="text-align:center;">
  <img src="./data-markdown/pics/shacl_processor_basic.svg" height="500">
</div>


+++

**Turtle Revision** <!-- .element: style="font-size:50px; margin-bottom:1.5em;" --> <br>

<ul>
  <li class="fragment">Property List Notation

  <pre><code class="language-turtle">
  :s :p :o ;
     :q :o .
  </code></pre>

  </li>
  <li class="fragment">Blank Node Notation

  <pre><code class="language-turtle">
  [:p []] .
  </code></pre>

  </li>
  <li class="fragment">RDF List Notation

  <pre><code class="language-turtle">
  :s :p (1 2 3).
  </code></pre>

  </li>
</ul>


+++


**Digression: RDF List Type** <!-- .element: style="font-size:50px; margin-bottom:1.5em;" --> <br>

<div class="fragment">
<pre><code class="language-turtle">:s :p (1 2 3).</code></pre>
</div>

<div class="fragment">

<pre><code data-trim class="language-turtle"><script type="text/template">

:s :p _:genid1 .

_:genid1 rdf:first "1"^^xsd:integer ;
         rdf:rest  _:genid2 .

_:genid2 rdf:first "2"^^xsd:integer ;
         rdf:rest  _:genid3 .

_:genid3 rdf:first "3"^^xsd:integer ;
         rdf:rest  rdf:nil .

</script></code></pre>
</div>

+++


**Practical** <!-- .element: style="font-size:50px; margin-bottom:1.5em;" --> <br>

<ul>
        <li class="fragment"> Go to <a href="https://tinyurl.com/shacl-gist"> https://tinyurl.com/shacl-gist </a> </li>
        <li class="fragment"> Example 1: Follow the link to the SHACL Playground </li>
        <li class="fragment"> Exercise: Fix the data and make the shapes pass! <div style="text-align:center; margin-top:0.5em;"> 🐱‍💻 ✅ </div> </li>
</ul>
