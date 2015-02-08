# Nathan-Bateman.github.io
EXTERNAL RESOURCES AND HONOR CODE:

http://www.textfixer.com/html/compress-html-compression.php
http://cssminifier.com/
http://jscompress.com/
https://developers.google.com/speed/docs/insights/about - many pages from in here
https://piazza.com/class/i0sf6tsmg0r7do?cid=1017
http://davidwalsh.name/translate3d
https://msdn.microsoft.com/en-us/library/ie/jj200286(v=vs.85).aspx
http://www.smashingmagazine.com/2013/06/10/pinterest-paint-performance-case-study/
https://docs.webplatform.org/wiki/css/functions/translateX()
http://www.html5rocks.com/en/tutorials/speed/rendering/#toc-raf
http://www.html5rocks.com/en/tutorials/speed/scrolling/
http://www.html5rocks.com/en/tutorials/developertools/revolutions2013/#toc-paint-rectangles
http://addyosmani.com/blog/making-a-site-jank-free/
https://developer.chrome.com/devtools/docs/timeline
https://piazza.com/class/i0sf6tsmg0r7do?cid=1141
https://piazza.com/class/i0sf6tsmg0r7do?cid=1073
https://piazza.com/class/i0sf6tsmg0r7do?cid=968
http://www.paulirish.com/2012/why-moving-elements-with-translate-is-better-than-posabs-topleft/
http://ripley6811.github.io/frontend-nanodegree-mobile-portfolio/doc/index.html - viewed this page
as I was writing the read-me file, did not copy techniques, but was looking at how they explained 
replacing basicLeft with style.left in the function that generates the sliding pizzas

*many links embedded in the piazza posts I may have looked at but do not remember which they were
*I looked at one students repository, but I understood not what they had done, thus
	I did not use it en route to complete the project


“I hereby confirm that this submission is my work. 
I have cited above the origins of any parts of the 
submission that were taken from Websites, books, forums, 
blog posts, github repositories, etc. By including this in my email, 
I understand that I will be expected to explain my work in a video call 
with a Udacity coach before I can receive my verified certificate.”

To successfully run/test the relevant pages:

1. Navigate to the following url - https://developers.google.com/speed/pagespeed/insights/
2. Paste the following url - http://nathan-bateman.github.io/ - into the box in the center of the PSI page and click analyze
3. Observe results (the corresponding code is at the following location - https://github.com/Nathan-Bateman/Nathan-Bateman.github.io/blob/master/index_uncompressed.html
4. Paste the following url into your browser's address bar - http://nathan-bateman.github.io/views/pizza.html?#randomPizzas
5. Open Google Chrome Developer tools by pressing Ctrl+Shift+I on Windows or Cmd+Opt+I on Mac
6. Click on the "Timeline" Menu option and begin a recording by pressing the gray circle on the top/left side of the developer tools
7. Scroll down to the bottom, then back up to the top, and finally, click on the same circle (now red) again
8. Observe the FPS bars - most should be above 60 frames per second
9. Click on the "Console" Menu option then move the pizza slider to change the pizzas' sizes
10. Observe the "Time to resize pizzas" as they are logged to the console

NOTES:
All files referenced within the live pages have been compressed. The uncompressed files are marked "_uncompressed"
Or, if the minified file being used has been renamed, it is named 'filename_min' 

Files being used with the "min" added are: "style_min.css", "perfmattersmin.js", and "bootstrap-grid_min.css"

All other files being used in the live version maintain their original name, but an uncompressed version is still in the repository to make code-reading easier.

An outline of the changes made to main.js are as follows

-FOR changePizzaSizes(); - Removed each calculation involving the .randomPizzaContainer class to outside the loop and just did the calculations for the first item in the object since others in it would simply have the same size manipulations applied to them, rather than calculating them for each pizza to be manipulated on the page

-FOR updatePositions(); - stored the document.body.scrollTop / 1250; calculation to outside the loop as it does not change, for the "items" selecting the ".mover" class, and also the length of that array, I moved those variables to outside the function into the global scope, but it had to be after the moving pizzas were initially appended to the DOM and before updatePositions() was called. This is because the "items" variable queries and selects all the .mover classes on the page, but they are not appended until the end of the main.js file. Thus, to find them they would have to be there, but they are not if the "items" variable is not defined at the end of the file (after the initial placement of the .mover pizzas on the page) but before the updatePositions(); function is called. 

Additionally, I replaced the initial "elem.basicLeft = (i % cols) * s;" with "elem.style.left = ((i % cols) * s) + 'px';". This is because in the updatePositions() function, the css transform/translate3d was implemented to manipulate the location of the sliding pizzas, rather than just changing the location each time using "style.left." Thuse style.left was no longer changing the location of items with each iteration, but used only to set the initial positions of the sliding pizzas.

The transform/translate3d works to move the pizzas across the page upon a scroll and recalculates the x value for each item in the iteration (the .mover classed pizzas). The 3d function is used to increase power from the hardware as it is calculated using the GPU rather than the CPU.
