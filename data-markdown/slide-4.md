**SHACL: Describing Graphs** <!-- .element: style="font-size:75px; margin-bottom:1.5em;" --> <br>


+++

<blockquote style="width: 100%; margin: 1.5em 0; font-size: 1.1em; line-height: 1.6; font-style: italic; text-align: left; border-left: 3px solid #999; padding: 0.3em 0 0.3em 1.2em; box-sizing: border-box;">
  “Shapes Constraint Language (SHACL) is a World Wide Web Consortium (W3C) standard language for describing Resource Description Framework (RDF) graphs.”
</blockquote>
<p style="text-align: right; font-style: normal; font-size: 0.85em; margin-top: 0.5em;">— Wikipedia, <em>SHACL</em></p>

+++

<blockquote style="width: 100%; margin: 1.5em 0; font-size: 1.1em; line-height: 1.6; font-style: italic; text-align: left; border-left: 3px solid #999; padding: 0.3em 0 0.3em 1.2em; box-sizing: border-box;">
  “As SHACL shape graphs are used to validate that data graphs satisfy a set of conditions they can also be viewed as a description of the data graphs that do satisfy these conditions.
</blockquote>

+++

<blockquote style="width: 100%; margin: 1.5em 0; font-size: 1.1em; line-height: 1.6; font-style: italic; text-align: left; border-left: 3px solid #999; padding: 0.3em 0 0.3em 1.2em; box-sizing: border-box;">
  Such descriptions may be used for a variety of purposes beside validation, including user interface building, code generation and data integration.”
</blockquote>
<p style="text-align: right; font-style: normal; font-size: 0.85em; margin-top: 0.5em;">— SHACL Spec, <em>Abstract</em></p>


+++


<div style="position: relative; height: 100vh;">
  <img src="./data-markdown/pics/releven.svg" style="height: 100%; width: 100%; object-fit: contain; transform: scale(2.5);">
  <img class="fragment" src="./data-markdown/pics/math.gif" style="position: absolute; top: 10%; right: 0; width: 25%; height: auto;">
</div>


+++

**SHACL Compact Syntax** <!-- .element: style="font-size:60px; margin-bottom:1.5em;" --> <br>


<div class="fragment">
<blockquote style="width: 100%; margin: 1.5em 0; font-size: 1.1em; line-height: 1.6; font-style: italic; text-align: left; border-left: 3px solid #999; padding: 0.3em 0 0.3em 1.2em; box-sizing: border-box;">
The Compact Syntax offers an alternative notation to the general RDF-based notations for SHACL, aimed at human editors and readers. 
</blockquote>
<p style="text-align: right; font-style: normal; font-size: 0.85em; margin-top: 0.5em;">— SHACL Compact Syntax Spec, <em>Abstract</em></p>
</div>



+++

<b>λ</b>

```ttl
 shape ex:PersonShape -> ex:Person {
	ex:ssn       xsd:string [0..1] pattern="^\\d{3}-\\d{2}-\\d{4}$" .
	ex:worksFor  IRI ex:Company [0..*] .
 }
```