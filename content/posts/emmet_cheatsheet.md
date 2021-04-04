+++
categories = ["emmet", "text-editor"]
date = "2021-04-04"
description = "Emmet Cheatsheet"
title = "Emmet Cheatsheet"
+++

Emmet is a plugin for text editors, it is already included in VS Code and can be installed in Sublime, Atom, Vim, etc.

Emmet is usefull in writing HTML and CSS in less words, following is the list of emmet shortcut that I use daily.

<kbd>!</kbd> <kbd>TAB</kbd>: This will create a empty HTML scaffold with `head`, `body` and meta tags.

<kbd>li*5</kbd> <kbd>TAB</kbd>: This will create 5 li tags

<kbd>li*5{Item $}</kbd> <kbd>TAB</kbd>: This will create 5 li and everyone will have text saying Item 1 to Item 5

<kbd>.product</kbd> <kbd>TAB</kbd>: This will create a div with class product.

<kbd>option[value=$]{$}*31</kbd> <kbd>TAB</kbd>: Option with value option till 31, can be used for date option

<kbd>span.product</kbd> <kbd>TAB</kbd>: This will create a span with class product.
<kbd>ul.product</kbd> <kbd>TAB</kbd>: This will create a ul with class product.

<kbd>table>thead>tr>th*5^^tbody>tr*4>td*5^^tfoot>tr></kbd> <kbd>TAB</kbd>: This will create a table with 5 Column with thead, tbody and tfoot element.