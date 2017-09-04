---
layout: post
title:  Swap elements in dom by drag and drop.
date:   2017-05-15 16:47:14 +0000
---



Drag and drop is a very common feature. In which you drag an element and drop it somewhere else.
Drag and drop is a standard feature in HTML5, You can make any element draggable.
Below are the steps on how to achieve the same.
<!--more-->
#### Below is a demo of the same (drag div1 to div2).
<div class="drag-demo">
  <script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>
  <script>
    function drag(ev)
    {ev.dataTransfer.setData('target_id',ev.target.id);}
    function allowDrop(ev) {
 	    ev.preventDefault();
 	    }
      function drop(ev) {
        var drop_target = ev.target;
        var drag_target_id = ev.dataTransfer.getData('target_id');
        var drag_target = $('#'+drag_target_id)[0];
        var tmp = document.createElement('span');
        tmp.className='hide';
        drop_target.before(tmp);
        drag_target.before(drop_target);
        tmp.replaceWith(drag_target);
      }
  </script>
  <div class="draggable-div" id="div1"
  ondrop="drop(event)" ondragover="allowDrop(event)" draggable="true" ondragstart="drag(event)">Div 1</div>
  <div class="draggable-div light" id="div2"
    ondrop="drop(event)" ondragover="allowDrop(event)" draggable="true" ondragstart="drag(event)">Div 2</div>
</div>

---
## First step: Make the elements draggable we want to drag
{% highlight html %}
<div id="div1" draggable=true>Div 1</div>
<div id="div2" draggable=true>Div 2</div>
{% endhighlight %}
## Second step: Save the id of dragged element
{% highlight js %}
function drag(event)
  {
    event.dataTransfer.setData
    ('target_id',ev.target.id);
  }
{% endhighlight %}
`event.dataTransfer` will be available in whole drag and drop event, so it can be used to keep dragged target id.        
drag function can be called by attribute `ondragstart`, which will call drag function passing event as a argument.
{% highlight html %}
<div id="div1" draggable=true ondragstart="drag(event)">Div 1</div>
{% endhighlight %}

## Third step: Allow element to be dropped in other element
By default elemets can't be dropped in other element, so to prevent this default behaviour
call allowDrop function by attribute `ondragover`.
{% highlight js %}
function allowDrop(event)
  {
  event.preventDefault();
  }
{% endhighlight %}
{% highlight html %}
<div id="div1" draggable=true ondragstart="drag(event)" ondragover="allowDrop(event)">Div 1</div>
{% endhighlight %}

## Fourth Step: Swap elements on dropping the element
`ondrop` attribute is fired on which a element is dropped, call drop function by `ondrop` attribute.
{% highlight html %}
<div id="div1" draggable=true ondragstart="drag(event)" ondragover="allowDrop(event)" ondrop="drop(event)">Div 1</div>
{% endhighlight %}
In drop function swap drag_target with drop_target to achieve desired result.
{% highlight js %}
function drop(event) {
  event.preventDefault();  
  var drop_target = event.target;
  var drag_target_id = ev.dataTransfer.getData('target_id');
  var drag_target = $('#'+drag_target_id)[0];
  var tmp = document.createElement('span');
  tmp.className='hide';
  drop_target.before(tmp);
  drag_target.before(drop_target);
  tmp.replaceWith(drag_target);
}
{% endhighlight %}
drop function code explanation:
- `event.preventDefault()` is to prevent default functionality of drop which is to open dropped element as a link.
- ` event.target` get element on which drop is made.
- `ev.dataTransfer.getData('target_id')` get id of dragged element from dataTransfer and by id get element.
- `document.createElement('span')` make dummy span which will help in swapping the elements.
- `drop_target.before(tmp)` append dummy span before drop_target in dom.
- `drag_target.before(drop_target)` append drop_target before drag_target in dom.
- `tmp.replaceWith(drag_target)` it will replace dummy span with drag_target.

code for swaping elements may seem over-conscious for two div's,     
But when there are more than two div's this is the best way to keep track of element's position.

#### Note
- Make sure your application has jquery loaded.     
To load jquery add      
`<script src="http://ajax.googleapis.com/ajax/libs/jquery/1.7.1/jquery.min.js" type="text/javascript"></script>`
 - I have made a typo mistake so that you don't just copy paste but instead understand the code.

#### source
- [w3schools](http://www.w3schools.com/html/html5_draganddrop.asp "w3schools"){:target="_blank"}
