---
layout: post
title:  What is icon font and why use it over png.
date:   2017-05-17 06:26:08 +0000
---


Problems with PNG or GIF files and using them as regular images for icons. 

1. **Size –** I had to create many different sized versions of the same icon which is inefficient and time consuming.
2. **Color –** I had to create big sprites of icons when I needed different colors of the same icons.
3. **Retina display –** every icon image needed another version for retina display which is also time consuming and more difficult to maintain.
4. **Effects –** there was a limited amount of effects I could do on images; for example, it wasn’t easy to make a smooth color transition.
5. **Exporting images –** exporting bigger sets of icons was really time consuming when I had too many icons and they were all designed in a specific style.
6. **Code –** there were many lines of code I had to manually type into my CSS to set up all the images under specific classes and sizes.
7. **Performance –** images add weight and more http requests which only slows down your entire website.

Well, what if I told you that **icon fonts** solve all of these problems and are super easy to use, maintain or even to create your own? Additionally, this new method is very well supported by all major browsers. So, let me first explain what an icon font is…

#### What is icon font?

Icon font is nothing more than a typical font that you’ve been already using in your projects. When you look closer into a font file, you’ll see that it’s just a table of characters. Each character is a vector shape. Now, you can simply replace those vector shapes representing characters with any shapes you want.

Using that method
1. **Create Your own-** you can create your own font full of your own shapes that can be used in the same way as you display text in HTML.
2. **Resize-** As you can assume, your icons can be resized to any size you want.
3. **Color-** you can easily change their color and even apply any CSS3 effects or animations like you would do on any text.
4. **Efficient-** Moreover, icon fonts are more efficient because they are not so heavy and require only one http request to load one font file.

<img src="http://imgh.us/iconfont-11.png" width="690" height="311"> 

Font icons fixed my problems with: size, color, retina display, effects, code and performance.

However, it was still difficult to maintain it and create my own sets.

[Fontastic.me comes to your rescue](http://fontastic.me/)