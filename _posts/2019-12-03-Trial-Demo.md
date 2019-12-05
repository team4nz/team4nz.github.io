---
layout: post
categories: posts
title: 2. Trial Demo
tags: [trial, demo, video]
date-string: DECEMBER 03, 2019
---
<script src="//ajax.googleapis.com/ajax/libs/jquery/1.9.1/jquery.min.js"></script>
<script>window.jQuery || document.write('<script src="_/js/libs/jquery-1.9.1.min.js"><\/script>')</script>

# Testing - Map
<center>
    <div class="photoset-grid-custom" data-layout="400">
        <img src="/images/map/manz-map.jpg">
    </div>
</center>

### idx3

> Trial 1
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/dUkFd7WjgtQ" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

> Trial 2
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/QFNBfKsfd44" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

### idx6

> Trial 1
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/O1pVHjuZYPI" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

> Trial 2
<center>
<iframe width="560" height="315" src="https://www.youtube.com/embed/qCVZcwHohbg" frameborder="0" allow="accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</center>

<script src="/assets/js/jquery.photoset-grid.js"></script>

<script type="text/javascript">
    $('.photoset-grid-custom').photosetGrid({
    // Set the gutter between columns and rows
    gutter: '5px',
  
    // Wrap the images in links
    highresLinks: true,
  
    // Asign a common rel attribute
    rel: 'print-gallery',

    onInit: function(){},
    
    onComplete: function(){
        // Show the grid after it renders
        $('.photoset-grid-custom').attr('style', '');
    }
});
</script>