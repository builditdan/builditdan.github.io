---
layout: post
title: Haml Tips
---

I have been working on a new Rails 5 application and have been using Haml for the first time. Really only used erb before. So in my learning I thought I would share a few examples for my reference and yours in the future.

## Buttons
Example when creating a button using the `button_to or link_to helper`. In this example I wanted to open a new tab to show a PDF. This button uses the bootstrap classes and glyph icons.

```
=button_to image_path(@pdf_name), type: "button", form_target: "_blank", class: "btn btn-md doc-button", method: "get" do`
%span{class: "glyphicon glyphicon-print"}
Print
```

```
=link_to image_path(@pdf_name), type: "button", target: "_blank", class: "btn btn-md doc-button", method: "get" do
          %span{class: "glyphicon glyphicon-print"}
          Print
```          

Also handy if you want to redirect back to a certain point wihtin the page using the html anchor property

`=link_to "Button1", some_path(a_var:"any value", anchor: 'some-location'),  method: "get"`


## iframe

Here I wanted to open ad PDF in a iframe

```
%div{class: "text-center"}
  %iframe{src: some_path(@a_var), width: "600", height: "780"}
```

## Drop Down Button

Here is example of a dropdown button with a action back to a controller

```
%span{class: "dropdown-container"}
  %button{class: "btn btn-md doc-button dropdown-toggle", type: "button", "data-toggle" => "dropdown"}
    Select Something
      %span{class: "caret"}
        %ul{class: "dropdown-menu"}
          %li
            =link_to "Hide", some_path(a_var:"hide"), method: "get"
            -@a_array.each do |name|
              =link_to name[0], some_path(a_var:name[1], anchor: 'property-location'),  method: "get"
```


Dan

Feel free to [contact me](http://builditdan.github.io/contact.html) with any questions you may have
