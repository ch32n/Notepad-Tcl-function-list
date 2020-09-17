# Notepad++ Tcl function list

Tcl parser for notepad++ function list. Supports tcl procedures, namespaces, classes and methods.

## How to activate

Edit FunctionList.xml in %appdata%\notepad++ or installation folder of notepad++ (FunctionList.xml in %appdata%\notepad++ should be deleted in this case).

Add tcl language association to \<associationMap>

```
<association id= "tcl_syntax" langID="29"/>
```

Add tcl parser to \<parsers>

```
<parser id="tcl_syntax" displayName="TCL" commentExpr="(#)">
    <classRange
        mainExpr="^[\t ]*((oo::(class|abstract)[\s]+create)|(namespace[\s]+eval))[\s]+[^\n]+\{"
        openSymbole = "\{"
        closeSymbole = "\}"
        displayMode="node">
        <className>
            <nameExpr expr="(create|eval)[\t ]+[\w:_\-.]+"/>
            <nameExpr expr="[\t ]+[\w:]+"/>
            <nameExpr expr="[\w:]+"/>
        </className>
        <function
            mainExpr="^[\t ]*(((proc|((private|public)\s)?method)\s+[\x21-\x7E]+)|constructor|destructor)[^\n]+?\{">
            <functionName>
                <funcNameExpr expr="[\w_\-.]+[\s]+\{"/>
                <funcNameExpr expr="[\w_\-.]+"/>
            </functionName>
        </function>
    </classRange>
    <function
        mainExpr="^[\t ]*(((proc|((private|public)\s)?method)\s+[\x21-\x7E]+)|constructor|destructor)[^\n]+?\{">
        displayMode="$className->$functionName">
        <functionName>
            <nameExpr expr="[\w_\-.]+[\s]+\{"/>
            <nameExpr expr="[\w_\-.]+"/>
        </functionName>
        <className>
            <nameExpr expr="([\w_\-.]+((::[\w_\-.]+)+)?)(?=[\s]*::)"/>
        </className>
    </function>
</parser>
```

Restart notepad++
