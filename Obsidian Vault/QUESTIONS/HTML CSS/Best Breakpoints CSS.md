```scss
@media (min-width:320px)  { /* smartphones, iPhone, portrait 480x320 phones */ }
@media (min-width:481px)  { /* portrait e-readers (Nook/Kindle), smaller tablets @ 600 or @ 640 wide. */ }
@media (min-width:641px)  { /* portrait tablets, portrait iPad, landscape e-readers, landscape 800x480 or 854x480 phones */ }
@media (min-width:961px)  { /* tablet, landscape iPad, lo-res laptops ands desktops */ }
@media (min-width:1025px) { /* big landscape tablets, laptops, and desktops */ }
@media (min-width:1281px) { /* hi-res laptops and desktops */ }
```

In practice, many designers convert pixels to **em**, largely because **em** afford better zooming. At standard zoom **1em === 16px**, multiply pixels by **1em/16px** to get **em**. For example, **320px === 20em**.

In response to the comment, **min-width** is standard in "mobile-first" design, wherein you start by designing for your smallest screens, and then add ever-increasing media queries, working your way onto larger and larger screens.

Regardless of whether you prefer **min-, max-**, or combinations thereof, be cognizant of the order of your rules, keeping in mind that if multiple rules match the same element, the later rules will override the earlier rules.