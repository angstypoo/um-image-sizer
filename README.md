# um-image-sizer
This is a Javascript utility for resizing images inside of a container in the dom

To use this plugin you need to include the file before any other javascript that utilizes the utility

* SUMMARY
 This utility gives you two methods for resizing images according to a parent container.
 It is intended to be used with a parent container that has predefined dimensions.  It requires the initial dimensions for the image, and the parent dimensions.
 It returns a string formatted for use with cssText.  There are two methods of resizing, zoom and center.  "Center" ensures that the larger of the two dimensions will expand to the
 container boundaries, while the smaller will be centered.  "Zoom" ensures that the smaller of the two dimensions will expand to the boundaries of the container, while the larger will be cropped
 with the image remaining centered.

 usage exaple:
 ```javascript
 var container = document.getElementById( mycountainerid );
 var image = document.getElementById( myimg );
 containerwidth = container.offsetWidth;
 containerheight = container.offsetHeight;
 imagewidth = image.naturalWidth;
 imageheight = image.naturalHeight;

 window.onresize = function() {
  image.style.cssText=umis.zoom(containerwidth, containerheight, imagewidth, imageheight);
  //the output will be "'height:'+imgHeight+'px;width:'+imgWidth+'px;margin-left:'+leftmargin+'px;margin-top:'+topmargin+'px;';
 };
 ```
 
 Alternatively, if you are using jquery:
  ```javascript
 function imagesizer() {
	var $container = $('div.class');
    var $containerheight = $container.height();
    var $containerwidth = $container.width();
    var $image = $('img.class');
    $($image).each(function() {
		var newcss=umis.zoom($containerwidth,$containerheight,this.naturalWidth,this.naturalHeight);
		this.style.cssText=newcss;
	});
 }
 $( window ).load(function() {
   imagesizer();
 });

 $( window ).resize(function() {
   imagesizer();
 });
 ```
 This example resizes all images according to a specified container
 Note that there is only one container specified-- this assumes that all containers will be the same size to reduce overhead.
 This use case is also good for carousels-- you should specify the active/visibile container as the container dimension reference because height() does not work on elements with display:none
