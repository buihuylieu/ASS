ASS.js is a parser for ASS file and renders subtitle on HTML5 video.

[DEMO](http://ass.woozy.im/)

[TODO list](https://github.com/weizhenye/ASS#todo)

# Usage
	<video id="video" src="example.mp4"></video>

	<script src="ass.js"></script>
	<script>
	  var x = new XMLHttpRequest();
	  x.open('GET', 'example.ass', 1);
	  x.onreadystatechange = function() {
	    if (x.readyState == 4 && x.status == 200) {
	      var ass = new ASS();
	      ass.init(x.responseText, document.getElementById('video'));
	    }
	  }
	  x.send(null);
	</script>


# API

### Initialization
	var ass = new ASS();
	ass.init(content, video);
### Resize
	// If you change video's width or height, you should do
	ass.resize();
### Show
	ass.show();
### Hide
	ass.hide();


# TODO

Items with <del>strikethrough</del> means they won't be supported.

#### [Script Info]

* <del>Synch Point</del>
* <del>PlayDepth</del>
* __WrapStyle__: 0, 3
* __Collisions__: Reverse


#### [V4+ Styles]

There is no outline for text in CSS, text-stroke is webkit only and has poor performance, so I use text-shadow to replace outline.

#### [Events]

* <del>Picture</del>
* <del>Sound</del>
* <del>Movie</del>
* <del>Command</del>
* __Dialogue__
	+ __Effect__
		- <del>Karaoke</del> as an effect type is obsolete.
		- __Scroll up__
		- __Scroll down__
		- __Banner__
	+ __Text__ (override codes)
		- __\p__ use SVG
		- __\fsc[x/y], \fa[x/y], \fr[x/y/z]__ use matrix3d() in CSS
		- __\k, \kf, \ko, \kt, \K__ Karaoke
		- __\q__ WrapStyle: 0, 3
		- __\t([&lt;t1&gt;, &lt;t2&gt;, ][&lt;accel&gt;, ]&lt;style modifiers&gt;)__: &lt;accel&gt;, \2c, \3c, \4c, \2a, \3a, \4a, \bord, \xbord, \ybord, \shad, \xshad, \yshad, \clip, \iclip, \be, \blur
		- __\org(&lt;X&gt;, &lt;Y&gt;)__
		- __\clip(&lt;x1&gt;, &lt;y1&gt;, &lt;x2&gt;, &lt;y2&gt;)__
		- __\clip([&lt;scale&gt;, ]&lt;drawing commands&gt;)__
		- __\iclip(&lt;x1&gt;, &lt;y1&gt;, &lt;x2&gt;, &lt;y2&gt;)__
		- __\iclip([&lt;scale&gt;, ]&lt;drawing commands&gt;)__

#### <del>[Fonts]</del>
#### <del>[Graphics]</del>

# Known issues

* \N in libass has less height than &lt;br&gt; in browsers, subbers should avoid to use multiple \N to position a dialogue, use \pos instead.
* A dialogue with multiple \t is not rendered correctly, for transforms in browsers are order-sensitive.
* A dialogue with multiple rotations (\frx, \fry, \frz) is not rotated perfectly.
* text-shadow with different quantity of values can't be animated by CSS.
