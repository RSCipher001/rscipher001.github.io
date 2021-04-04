+++
categories = ["keyboard_shortcuts"]
date = "2021-04-04"
description = "How to use keyboard shortcuts to do more work by working smarter"
title = "My Favorite Editor Shortcuts For Faster Development"
+++

# Introduction

I work in a software company and everyday I see people doing easy things the hard way and getting tired, wasting time & energy, etc. When I say about mastering text editor shortcuts I don't want you to remember everything, I will be happy if you learn one shortcut per day, after a month you'll probably know more than 30 shortcuts and that's all you need, Let's see some of my favorite shortcuts, I have been using Sublime and VS Code but I'll try to list about other editors as well.

## Switching files

Almost all projects contain many files and during development we have to switch between files, a lot of people uses sidebar and they expand folder and choose file which is slow and time consuming process, let's see how to speed up.

Sublime & VS Code: <kbd>CTRL + P</kbd> opens fuzzy files finder, which means you can type partial names of your file to open it, ex: to open `resources/view/product/create.blade.php` you can type `rvpcre` and it will list on the first, after playing with this you'll love it.

IntelliJ IDEs: <kbd>Double Shift</kbd> and it will open file search option, File search in those IDEs can search for file name and also class name.

## Text Selection & Multi Selection

Text selection is the most common task in programming world, if you're a web developer then you have to repeat a lot of stuff in HTML like id, name then same variable for error message, etc. Knowing how to select text can save you a lot of time.

### Text Selection

These keyboard shortcuts are common for almost every editor and works on almost all platform (I don't have a Mac to test)
<table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col">#</th>
      <th scope="col">Shortcut</th>
      <th scope="col">Use</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th scope="row">1</th>
      <td><kbd>SHIFT + END</kbd></td>
      <td>From cursor to end of line</td>
    </tr>
    <tr>
      <th scope="row">2</th>
      <td><kbd>SHIFT + HOME</kbd></td>
      <td>From cursor to start of line</td>
    </tr>
    <tr>
      <th scope="row">3</th>
      <td><kbd>CTRL + SHIFT + LEFT/RIGHT ARROW KEY</kbd></td>
      <td>Select word by word form cursor</td>
    </tr>
    <tr>
      <th scope="row">5</th>
      <td><kbd>CTRL + BACKSPACE</kbd></td>
      <td>Delete word by word form left of cursor</td>
    </tr>
    <tr>
      <th scope="row">4</th>
      <td><kbd>CTRL + DELETE</kbd></td>
      <td>Delete word by word form right of cursor</td>
    </tr>
    <tr>
      <th scope="row">4</th>
      <td><kbd>SHIFT + DELETE</kbd></td>
      <td>Delete one line(May not work everywhere)</td>
    </tr>
  </tbody>
</table>