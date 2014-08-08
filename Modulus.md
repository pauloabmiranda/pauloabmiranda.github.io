---
layout: page
title: Modulus
published: true
---

This were taken from a post of <a href="http://www.gskinner.com/blog/archives/2008/05/core_as3_modulu.html" target="_blank">gskinner.com</a>.

**Using Modulus for Alternation**<br>
This is perhaps the simplest use case. Say you want to alternate row colors in a list - you can simply make the color of each row a function of the modulus value of the rowcount:

<code>
if (rowIndex % 2 == 0){<br>
&nbsp;&nbsp;rowColor = 0xFFFFFF;<br>
}else{<br>
&nbsp;&nbsp;rowColor = 0xCCCCCC;<br>
}
</code>

**Using Modulus to Vary Frequency**<br>
Similar to the above, you can use modulus to vary the frequency of execution of a block of code within a repeating block. For example:

<code>
// tick runs every frame:<br>
function tick(){<br>
&nbsp;&nbsp;trace("I run every frame");<br>
&nbsp;&nbsp;if (++frameCount % 10 == 0) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;trace("I run every 10 frames");<br>
&nbsp;&nbsp;}<br>
}
</code>

**Using Modulus to Wrap Values**<br>
You can also modulus to wrap a value within a specified range. For example, if you want to a sprite to move right, but wrap back to the left side of the screen when it hits the right side, you could use this:

`sprite.x = (sprite.x + 5) % stage.stageWidth;`

It's easy to modify this to work with negative x motion as well, you simply have to ensure the value is always positive:

`sprite.x = (sprite.x + velX + stage. stageWidth) % stage. stageWidth;`

**Using Modulus to Flatten Two Dimensional Data Sets**<br>
Creating two dimensional arrays by nesting arrays is very inefficient. It's much better to flatten the 2D data into a single array. You can do this easily using modulus and simple multiplication:

<code>
// iterate the array:<br>
function scanArray() {<br>
&nbsp;&nbsp;for (var i=0; i < flatArray.length; i++) {<br>
&nbsp;&nbsp;&nbsp;&nbsp;var x = i%columns;<br>
&nbsp;&nbsp;&nbsp;&nbsp;var y = Math.floor(i/columns);<br>
&nbsp;&nbsp;trace("value at x="+x+",y="+y+" is '"+flatArray[i]+"'");<br>
&nbsp;&nbsp;}<br>
}<br>
// access individual values:<br>
function getValueAt(x,y) {<br>
&nbsp;&nbsp;return flatArray[x+y*columns];<br>
}
</code>
