---
layout: doc
title: Processors
---


MMT uses several abstractions for processing content.
Implementations can be provided as [extensions](index.html) and are chosen based on appropriate identifiers (e.g., the format to which a parser is applicable).

Each abstraction comes with at least one main implementation, which is parametrized by a set of *rules*.
This allows a second (simpler but less flexible) way to customize MMT by supplying a different set of rules.
The type of rule depends on the processor (e.g., notations for a parser).

All processors are divided into three kinds. One kind handles structure (e.g., declarations) and one objects. The third kind pairs up a structure and an object processor. 

<table>
    <tr>
        <td/>
        <td/>
        <th colspan="4">abstract interface</th>
        <th colspan="3">main implementation(s)</th>
    </tr>
    <tr>
        <th>process</th>
        <th>level</th>
        <th>class (extends)</th>
        <th>identified by</th>
        <th>input</th>
        <th>output</th>
        <th>class</th>
        <th>parametrized by set of</th>
        <th>identifier</th>
    </tr>
    <tr>
        <th rowspan="3">parsing</th>
        <td>objects</td>
        <td><a href="apidoc://info.kwarc.mmt.api.parser.ObjectParser">ObjectParser</a></td>
        <td></td>
        <td>string with some extra data</td>
        <td>object</td>
        <td><a href="apidoc://info.kwarc.mmt.api.parser.NotationBasedParser">NotationBasedParser</a></td>
        <td>notations in scope</td>
        <td></td>
    </tr>
    <tr>
        <td>structure</td>
        <td><a href="apidoc://info.kwarc.mmt.api.parser.StructureParser">StructureParser</a></td>
        <td></td>
        <td>stream with some extra data</td>
        <td>document</td>
        <td><a href="apidoc://info.kwarc.mmt.api.parser.KeywordBasedParser">KeywordBasedParser</a></td>
        <td>keyword handlers</td>
        <td></td>
    </tr>
    <tr>
        <td>both</td>
        <td><a href="apidoc://info.kwarc.mmt.api.parser.Parser">Parser</a></td>
        <td>input format</td>
        <td></td>
        <td></td>
        <td colspan="2"><pre>new KeywordBasedParser(new NotationBasedParser)</pre></td>
        <td>"mmt"</td>
    </tr>
    <tr>
        <th rowspan="3">checking</th>
        <td>objects</td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.ObjectChecker">ObjectChecker</a></td>
        <td></td>
        <td>object with unknown parts</td>
        <td>object with unknown parts inferred</td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.RuleBasedChecker">RuleBasedChecker</a></td>
        <td>typing rules in scope</td>
        <td></td>
    </tr>
    <tr>
        <td>structure</td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.StructureChecker">StructureChecker</a></td>
        <td></td>
        <td>structural element</td>
        <td>nothing</td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.MMTStructureChecker">MMTStructureChecker</a></td>
        <td>not parametrized</td>
        <td></td>
    </tr>
    <tr>
        <td>both</td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.Checker">Checker</a></td>
        <td>id</td>
        <td></td>
        <td></td>
        <td colspan="2"><pre>new MMTStructureChecker(new RuleBasedChecker)</pre></td>
        <td>"mmt"</td>
    </tr>
    <tr>
        <th rowspan="3">simplification</th>
        <td>objects</td>
        <td><a href="apidoc://info.kwarc.mmt.api.uom.ObjectSimplifier">ObjectSimplifier</a></td>
        <td></td>
        <td>object</td>
        <td>simplified object</td>
        <td><a href="apidoc://info.kwarc.mmt.api.uom.RuleBasedSimplifier">RuleBasedSimplifier</a></td>
        <td>simplification rules in scope</td>
        <td></td>
    </tr>
    <tr>
        <td>structure</td>
        <td><a href="apidoc://info.kwarc.mmt.api.uom.StructureSimplifier">StructureSimplifier</a></td>
        <td></td>
        <td>structural element</td>
        <td>list of declarations</td>
        <td><a href="apidoc://info.kwarc.mmt.api.uom.ElaborationBasedSimplifier">ElaborationBasedSimplifier</a></td>
        <td>structural features in scope</td>
        <td></td>
    </tr>
    <tr>
        <td>both</td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.Checker">Simplifier</a></td>
        <td>id</td>
        <td></td>
        <td></td>
        <td colspan="2"><pre>new ElaborationBasedSimplifier(new RuleBasedSimplifier)</pre></td>
        <td>"mmt"</td>
    </tr>
    <tr>
        <th>interpretation</th>
        <td></td>
        <td><a href="apidoc://info.kwarc.mmt.api.checking.Interpreter">Interpreter</a> (<a href="apidoc://info.kwarc.mmt.api.archives.Importer">Importer</a>)</td>
        <td>input format</td><td colspan="2">triple of parser, checker, and simplifier</td>
        <td colspan="2">
<pre>
new TwoStepInterpreter(
  new KeywordBasedParser(new NotationBasedParser),
  new MMTStructureChecker(new RuleBasedChecker),
  new ElaborationBasedSimplifier(new RuleBasedSimplifier)
)</pre></td>
        <td>"mmt"</td>
    </tr>
    <tr>
        <th rowspan="3">presentation</th>
        <td>objects</td>
        <td><a href="apidoc://info.kwarc.mmt.api.presentation.ObjectPresenter">ObjectPresenter</a></td>
        <td></td>
        <td>object</td>
        <td>according to format</td>
        <td><a href="apidoc://info.kwarc.mmt.api.presentation.NotationBasedPresenter">NotationBasedPresenter</a> <a href="apidoc://info.kwarc.mmt.api.presentation.MathMLPresenter">MathMLPresenter</a></td>
        <td>notations in scope</td>
        <td></td>
    </tr>
    <tr>
        <td>structure</td>
        <td><a href="apidoc://info.kwarc.mmt.api.presentation.StructurePresenter">StructurePresenter</a></td>
        <td></td>
        <td>structural element</td>
        <td>according to format</td>
        <td><a href="apidoc://info.kwarc.mmt.api.presentation.MMTStructurePresenter">MMTStructurePresenter</a> <a href="apidoc://info.kwarc.mmt.api.presentation.HTMLPresenter">HTMLPresenter</a></td>
        <td>not parametrized</td>
        <td></td>
    </tr>
    <tr>
        <td>both</td>
        <td><a href="apidoc://info.kwarc.mmt.api.presentation.Presenter">Presenter</a> (<a href="apidoc://info.kwarc.mmt.api.archives.Exporter">Exporter</a>)</td>
        <td>output format</td>
        <td></td>
        <td></td>
        <td colspan="2">
<pre>
new MMTStructurePresenter(new NotationBasedPresenter)
new HTMLPresenter(new MathMLPresenter)</pre></td>
        <td>"present-text-notations"<br/>"html"</td>
    </tr>
</table>
