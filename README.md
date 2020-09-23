﻿<div align="center">

## Image Resize \(Aspect Ratio, Actual Resize\)


</div>

### Description

I've search the PHP codes, found two folks who have published resize code. Problem with one , is that it only gives you the new size but you set it in the HTML's IMG tag, which is dumb in my opinion because you still are downloading the entire image. Another submision did the same, except you could use a width, but they did a loop decreasing the size times .5 until it was close as it can get to the width you wanted, problem with this was it was slow. In either case neither actually resized the image just defined a new size. I took an hour did some reasearch at php.net, and found basic information to make this code.
 
### More Info
 
Edit the $picsize to give desired width of each thumbnail.

also passing img_name with the path and filename of the image you want to resize.

for example gd.php?img_name=zoom.jpg

I wrote this using PHP 4.1.2 Win32 binaries, which includes an extension called php_gd.dll in the extension folder, you can enable this in your php.ini, if your PHP does not have this you may be able to obtain this dll at php4win.com, otherwise you will have to recompile your PHP binaries from the source with the GD libraries.

The code will cause it to send Jpeg data back to the browser resized, allowing you to send a few kilobytes rather than 300K or so if you just told HTML how big you wanted to shrink it.

none that I am aware of. because you define width only, if your images are a wide range of different heights they may look odd next to each other in a thumbnail listing.


<span>             |<span>
---                |---
**Submitted On**   |
**By**             |[Karl Blessing](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByAuthor/karl-blessing.md)
**Level**          |Beginner
**User Rating**    |4.4 (31 globes from 7 users)
**Compatibility**  |PHP 4\.0
**Category**       |[Graphics/ Sound](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByCategory/graphics-sound__8-15.md)
**World**          |[PHP](https://github.com/Planet-Source-Code/PSCIndex/blob/master/ByWorld/php.md)
**Archive File**   |[](https://github.com/Planet-Source-Code/karl-blessing-image-resize-aspect-ratio-actual-resize__8-570/archive/master.zip)





### Source Code

```
<?
/* Informs the browser the data being sent back is a Jpeg Image */
Header ("Content-type: image/jpeg");
/* loads image passed thru script
ie: gd.php?img_name=zoom.jpg */
$src_img = imagecreatefromjpeg($img_name);
/* desired width of the thumbnail */
$picsize = 123;
/* grabs the height and width */
$new_w = imagesx($src_img);
$new_h = imagesy($src_img);
/* calculates aspect ratio */
$aspect_ratio = $new_h / $new_w;
/* sets new size */
$new_w = $picsize;
$new_h = abs($new_w * $aspect_ratio);
/* creates new image of that size */
$dst_img = imagecreate($new_w,$new_h);
/* copies resized portion of original image into new image */
imagecopyresized($dst_img,$src_img,0,0,0,0,$new_w,$new_h,imagesx($src_img),imagesy($src_img));
/* return jpeg data back to browser */
imagejpeg($dst_img);
?>
```

