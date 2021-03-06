PLEASE NOTE I've imported this repository to GitHub because I still receive
requests related to it. I do not intend to further maintain it actively. If
you are interested in working on the code I will happily give you full access
to the repository, just drop me a note (svenfuchs@artweb-design.de or send me
a GitHub message). I also might help you out with advise or pointers but I
sadly can not invest tons of time into it.

Tag Cloud Plugin For Mephisto
=============================

This plugin allows you to display a tag cloud in your Mephisto templates. It is, as of writing, the most complete, sophisticated, standard-conform and allover-awesome implementation of a tag cloud plugin for Mephisto. You guessed it, I'm biased ;)

The architecture of this plugin (i.e. the implementation as a custom Liquid tag) is based on the Boldr tag cloud plugin by Nicolas Mérouze which can be found at: http://svn.boldr.net/mephisto/plugins/trunk/mephisto_tag_cloud/. 

Usage
=====

Install the plugin:

	ruby script/plugin install git://github.com/svenfuchs/mephisto_tag_cloud.git
	
Thereafter you can use a dedicated liquid tag, 'tagcloud', in your templates like this:

	<ul class="tagcloud">
	{% tagcloud as tag %}
		<li>{{ tag | link_to_tag }}</li>
	{% endtagcloud %}
	</ul>
	
We use CSS to define the formatting. Just define classes like these in your stylesheets:

	.tagcloud .weight-1 { font-size: 10px; }
	.tagcloud .weight-2 { font-size: 11px; }
	.tagcloud .weight-3 { font-size: 12px; }
	.tagcloud .weight-4 { font-size: 13px; }	
	
Options
=======
	
You can configure the number of sizes/weights that are generated through the option:

	TagCloud.weights = 6 # default: 10

This get's you a distribution over 6 sizes.

You can configure whether the tags are ordered alphabetically or by the weight of the tag by using:

	TagCloud.order = :alpha  # default
	TagCloud.order = :weight

You can specify the distribution method that is used to distribute the tags over the weights by using:

	TagCloud.method = :log		# logarithmic distribution
	TagCloud.method = :linear	# linear (weights share same range of counts)
	TagCloud.method = lambda {|number| ... } 	# custom: specify your own

Tag cloud distribution graph
============================

To visualize the distribution of your tags/weights and play around with the options, you can add this to your routes:

# config/routes.rb
map.connect 'tagcloud/distribution', :controller => 'tag_cloud', :action => 'distribution'

Afterwards you can access a simple distribution graph at (e.g.) http://localhost:3000/tagcloud/distribution

	
Licence and support
===================
	
(C) 2007 Sven Fuchs, under an MIT licence. http://www.opensource.org/licenses/mit-license.php

Please leave any bugs or feedback at http://www.artweb-design.de
