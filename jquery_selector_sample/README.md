This sample shows you how to specify the correct externs file to use JSlim with a jQuery pseudo selector.  

Running this sample
--------------------------------------

Once you have built JSlim you can compile this example by running the following command from the root of the JSlim project tree:

<pre><code>build/install/jslim/bin/jslim --js_output_file jquery_selector_sample/out.js --js jquery_selector_sample/main.js --lib_js libs/jquery-1.7.2.js --externs jquery_selector_sample/externs.txt</code></pre>

Then open the index.html file in your favorite browser.

Why is this sample special?
--------------------------------------

JSlim has many samples using jQuery, but this one is special because of the use of pseudo selectors.  This sample removes a class from every other paragraph tag using the `:odd` pseudo selector.  jQuery powers these selectors with a set of functions in the Sizzle library.  The final code looks like this:

<pre><code>jQuery(document).ready(function() { 
    $("p:odd").removeClass("blue").removeClass("under"); 
});</code></pre>

This code works by calling the `odd` function from jQuery, but it doesn't directly reference it.  The Sizzle library calls the `odd` function dynamically by parsing the selector string.  JSlim can't follow that dynamic reference so it thinks that the `odd` function isn't getting called and removes it.  

You need to specify an externs file for JSlim so it knows to keep the `odd` function.

Extern files
--------------------------------------

JSlim follows a similar convention to the Google Closure Compiler with an externs file.  It's the last argument in the build command from the first section.  This file lists a set of functions that JSlim should never remove.  The externs file for this sample looks like:

<pre><code>find
TAG
odd</code></pre>

This preserves the odd function and the functions that support it and makes the sample work properly.
