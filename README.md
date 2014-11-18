PersonalProject

The key idea of my project is that I leveraged open-source resources that are available online to expedite improved usability of my webpage.

I wanted to create a webpage that I could easily filter through Pac-12 football stats. My brother does a Pac-12 Fantasy Football League so I wanted 1 page to have all the stats available to me via tabs that I synced to different stat leaders by position in the Pac-12. I also used a jQuery to create a countdown at the heading of the page that always counts down to when the rosters are due to my brother each week. Below describes in more detail about how the page functions.

The tabs are created using javascript code that is derived from the jQuery javascript library (http://jquery.com/). Specifically, it uses jQueryUI (http://jqueryui.com/), which is a "curated set of user interface interactions,	effects, widgets, and themes built on top of the jQuery JavaScript Library." 

It is essentially a library of pre-written javascript code snippets that perform common user interface functions on a website (tabs, date pickers, menus, progress bars). Instead of an individual having to write all the code from scratch, they can download and call the code from the library.

The tabs functionality (http://jqueryui.com/tabs/) has a basic functionality like we use. There's a bunch of additional functions that can be implemented as well (collapsible content, vertical tabs, closing tabs, etc). 

To invoke the jquery library in my html page, I added the script calls in the HTML header:
        <script type="text/javascript" src="data/js/jquery.js"></script>
        <script type="text/javascript" src="data/js/jquery-ui.js"></script>


In the style section of the header, I defined what the tabs will look like:

	<style>
            html {
                font-size:10px;
            }
            .iframetab {
                width:100%;
                height:auto;
                border:0px;
                margin:0px;
                background:url("data/asu.png");
                position:relative;
                top:-1px;
            }
            .ui-tabs-panel {
                padding:5px !important;
            }
            .openout {
                float:right;
                position:relative;
                top:-28px;
                left:-5px;
            }
        </style>

And finally in the script section of the header, I have the actual script for the tabs that define the functionality. Note that this script calls specific functions from the jQueryUI library invoked above. For example, "function.getSelectedTabIndex()" is a function whose code resides in the jQueryUI library. I didn't need to code that, it already existed in the library. Big time saver!

	<script>
            $(document).ready(function() {
                var $tabs = $('#tabs').tabs();
                //get selected tab
                function getSelectedTabIndex() {
                    return $tabs.tabs('option', 'selected');
                }
                //get tab contents
                beginTab = $("#tabs ul li:eq(" + getSelectedTabIndex() + ")").find("a");
                loadTabFrame($(beginTab).attr("href"),$(beginTab).attr("rel"));
                $("a.tabref").click(function() {
                    loadTabFrame($(this).attr("href"),$(this).attr("rel"));
                });
                //tab switching function
                function loadTabFrame(tab, url) {
                    if ($(tab).find("iframe").length == 0) {
                        var html = [];
                        html.push('<div class="tabIframeWrapper">');
                        html.push('<div class="openout"><a href="' + url + '"><img src="data/world.png" border="0" alt="Open"                        title="Remove iFrame" /></a></div><iframe class="iframetab" src="' + url + '">Load Failed?</iframe>');
                        html.push('</div>');
                        $(tab).append(html.join(""));
                        $(tab).find("iframe").height($(window).height()-80);
                    }
                    return false;
                }
            });
        </script>

In the body, I defined how many tabs there are, and to what they link.A <div> is simply a section of a document. <ul> is an unordered list, with each <li> being an item in that list. 

		<div id=tabs> is the section of the document that contains the tabs
		<div id=tabs-1> through <div id=tabs-3> is the section of the document taken up by each tab.

		<body>
		<div id="tabs">
            	<ul>
                	<li><a class="tabref" href="#tabs-1" rel="http://www.espn.com">ESPN</a></li>
                	<li><a class="tabref" href="#tabs-2" rel="http://www.espn.com">ESPN</a></li>
                	<li><a class="tabref" href="#tabs-3" rel="http://www.espn.com">ESPN</a></li>
		
        	 </ul>
            		<div id="tabs-1" class="tabMain">
            		</div>
            		<div id="tabs-2">
            		</div>
        		<div id="tabs-3">
            		</div>
        	</div> 
		</body>

Hope you like it.

Thanks,

Matt Henderson
