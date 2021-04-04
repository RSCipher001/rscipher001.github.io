---
title: "Emmet Cheatsheet"
date: 2019-11-10T00:23:02+05:30
description: "Emmet cheatsheet contains shortcuts that can be used to quicky create markup data"
tags: [emmet]
category: [Tips]
---

Emmet is a plugin for text editors, it is already included in VS Code and can be installed in Sublime, Atom, Vim, etc.

Emmet is usefull in writing HTML and CSS in less words, following is the list of emmet shortcut that I use daily.

Shortcut    | Usage
------------|------
! TAB       | This will create a empty HTML scaffold with `head`, `body` and meta tags.
li * 5 TAB  | This will create 5 li tags


li*5{Item $} TAB: This will create 5 li and everyone will have text saying Item 1 to Item 5

.product TAB: This will create a div with class product.

option[value=$]{$}*31 TAB: Option with value option till 31, can be used for date option

span.product TAB: This will create a span with class product.
ul.product TAB: This will create a ul with class product.

table>thead>tr>th*5^^tbody>tr*4>td*5^^tfoot>tr> TAB: This will create a table with 5 Column with thead, tbody and tfoot element.