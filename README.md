Download Link: https://assignmentchef.com/product/solved-project-5-cpe101
<br>
For this project, you will implement three programs that transform images. No unittest required for this project.

<ul>

 <li>The first program will read an image file and write a new image revealing a hidden picture (puzzle.py).</li>

 <li>The second program will read an image file and write a new, “faded” version (fade.py).</li>

 <li>The third program will read an image file and write a new, blurred version of the image (blur.py).</li>

 <li>Your main program can call all these three programs (puzzle, fade, and blur).</li>

</ul>




<h1>Image File Format</h1>

The specific details for the three programs are discussed below. Each will process an image file stored in the <em>ppm</em> format. More specifically, your programs will process image files that conform to the P3 format discussed below. Note that all values written to P3 files (except the P3 header) <strong>must be integers</strong>. On the lab machines, you can view ppm files with either the <em>eog</em> program or the <em>gthumb </em>program (among others). Details of this format are provided on a separate <a href="http://netpbm.sourceforge.net/doc/ppm.html">ppm P3 format page</a><a href="http://netpbm.sourceforge.net/doc/ppm.html">.</a>

<h2><strong><em>Image File Format </em></strong></h2>

The P3 (.ppm) format is a text-based format (meaning that it is readable text) that defines an image as a sequence of pixels beginning with the top-left pixel and stored in row order (i.e. every pixel in a row is stored in left-to-right order and before any pixel in the next row).

A file conforming to the P3 format begins with header information. The header consists of the characters P3 , the integer width of the image (in pixels), the integer height of the image, and the maximum value for a color component (we will use 255 for this value). Immediately following the header is the color information for each pixel. A pixel’s color is represented by three integers denoting the red, green, and blue components (in that order). The following example shows how a file would look if it contained an image with one blue pixel, one red pixel, and one green pixel.

P3

3 1

255

0 0 255

255 0 0

0 255 0

…

The top-left pixel is said to be at location &lt;0, 0&gt; and the bottom-right at location &lt;width – 1, height – 1&gt; .

Note: if you use a program to create your own ppm files for testing, be sure to remove anything (such as comments) that does not conform to the expected format.




<h1>puzzle : program 1</h1>

Develop this first program in a file named puzzle.py. This program will get you started with the core functionality of processing a ppm image file. puzzle.py which contains function for decoding the image file.

<h2>Command-line Argument</h2>

Your program must take a single command-line argument that specifies the name of the input image file. If this argument is not provided, an appropriate usage message must be printed to the terminal and the program should terminate. This message is as follows:

Usage: python puzzle.py image_file.ppm

If, however, the image argument is provided but cannot be opened (e.g. does not exist), your program must print to the terminal:

Unable to open &lt;image&gt;

In this case, replace &lt;image&gt; with the name of the file passed in as an argument. You must use a try/except statement to perform this step.

<h2>Image Reading</h2>

For this program you must read a pixel, process the pixel, and then output the pixel before moving to the next pixel (in other words, you must not store all of the pixels at once). Recall that, in the ppm P3 format, each pixel is denoted by three integer values representing the pixel’s color components. Your program must not make any assumptions about the number of pixels or pixel components per line. This means that a line may contain many pixels or only a single pixel; likewise, a line may contain only the red and green components of a pixel with the blue component appearing on the next line.

<h2>Image Output</h2>

Your program will output the decoded image to a file named <em>hidden.ppm</em>. The output must be a valid P3 ppm image file.

Do not forget to write the required header information to your output file.

<h2>Solving the Puzzle</h2>

The puzzle image (shown below) hides a real image behind a mess of random pixels. In reality, the image is hidden in the red components of the pixels. <strong>Decode the image by increasing the value of the red component by multiplying it by 10</strong> (do not allow the resulting value to pass the maximum value of 255). In addition, set the green and blue components equal to the new red value. Shown below is the hidden image. It should be obvious once you have properly decoded the puzzle image. (If you are unsure, just ask.)

<h1>fade : program 2</h1>

This program is a relatively minor modification of the previous program.

Develop your program in a file named fade.py. The required functionality of your program is described below.

<h2>Command-line Arguments</h2>

Your program must take four command-line arguments (in the following order).

<ul>

 <li>The first specifies the name of the input image file.</li>

 <li>The second specifies <em>row</em> (y-coordinate)</li>

 <li>The third specifies <em>column</em> (x-coordinate) positions. 4) The last specifies the fade <em>radius</em>.</li>

</ul>

These last three arguments are expected to be integers. If these arguments are not provided, an appropriate usage message must be printed to the terminal and the program should terminate. This message is as follows:

Usage: python fade.py &lt;image&gt; &lt;row&gt; &lt;column&gt; &lt;radius&gt;

Your program will output the faded image to file name faded.ppm, which must be valid ppm file.

If, however, the image argument is provided but cannot be opened (e.g. does not exist), your program must print to the terminal:

Unable to open &lt;image&gt;

In this case, replace &lt;image&gt; with the name of the file passed in as an argument. You must use a try/except statement to perform this step.

<h2>Fading</h2>

This program will transform pixel values based on their distance from a specified point (this point may fall outside of the image). The <em>row</em> and <em>column</em> coordinates specified on the command-line give the point and the <em>radius</em> is used to control the fading.

For each pixel, compute the distance from the pixel location to the specified point. Scale (multiply) the color components of the pixel by <strong>(radius – distance) / radius</strong> (multiply the pixel components by this value). <strong>Do not</strong>, however, use a scale value below 20% (i.e., if the result of the scaling equation is less than 0.2, use 0.2; this prevents very dark borders around the image). Two examples are shown below. A link to the ppm file is provided, but the images shown in the browser are in png format.

Original image                                       <u>Faded version</u>  row=230, col=255, radius=255

Original image                      <u>Faded version</u>  row=160, col=200, radius=250

<h1>blur : program 3</h1>

This program is an extension of the type of processing done in the previous. In particular, this program will require storing the pixels of the image while processing.

Develop your program in a file named blur.py.

<h2>Command-line Arguments</h2>

Your program must take two command-line arguments (in the following order). The first specifies the name of the input image file. The second argument is optional. If provided, the second argument is an integer value specifying the “neighbor reach” to use in the blurring calculation (discussed below). This will allow a user to specify the amount of blurring. Your program will use this value to determine which neighbor pixels to consider in the averaging calculation.

If a second command-line argument is not present (i.e., the blur factor is not specified), then use a default value of 4. If the first argument is not provided, an appropriate usage message must be printed to the terminal and the program should terminate. This message is as follows:

Usage: python blur.py &lt;image&gt; &lt;OPTIONAL:reach&gt;

If, however, the image argument is provided but cannot be opened (e.g. does not exist), your program must print to the terminal:

Unable to open &lt;image&gt;

In this case, replace &lt;image&gt; with the name of the file passed in as an argument. You must use a try/except statement to perform this step.

<h2>Blurring</h2>

Once your program has read the contents of the image file, it will blur the image. This will be done by computing, for each pixel, the average of nearby pixels

(more precisely, the averages over each color component of the nearby pixels). A pixel’s blurred color will be determined by the colors of the pixels within a specified “neighbor reach”. The default “neighbor reach” is 4 (but this can be modified by a command-line argument as discussed previously). This means that a pixel’s blurred color will be determined by the colors of the pixels within four pixels to the left or right and within four pixels above or below (this will form a

square around the pixel). The diagram is meant to help illustrate.










In this diagram, we are trying to compute the color for the pixel in the center (the red element). Its neighbors (within a reach of 4) are all of the green elements. The pixels outside of this 9×9 square are not considered in the blurring calculation for this pixel. To compute the color for the center pixel, average the red, green, and blue components (independently) of every pixel in the 9×9 square (including the pixel itself; the red element in this diagram). Some pixels will not have the full complement of neighbors (such as those on or near the edge of the image). In these cases, just average the existing neighbors (i.e., those within the bounds of the image).

Two examples are shown below.




Original Image                                                                  <u>Blurred version</u> (reach of 4).







Original Image                                                                  <a href="http://users.csc.calpoly.edu/~dkauffma/cpe101/a6/lights_blur.ppm">Blurred version</a> (reach of 4).

<table width="637">

 <tbody>

  <tr>

   <td width="8"> </td>

   <td width="628">Submission</td>

  </tr>

 </tbody>

</table>

<strong>Submit all you py files in the PolyLearn. </strong>

<ul>

 <li>py</li>

 <li>py</li>

 <li>py</li>

 <li>py (your main program)</li>

 <li>Member Information</li>

</ul>