Templates
=============================  

Jekyll uses the Liquid templating language to process templates. All of the standard Liquid tags and filters are supported. Jekyll even adds a few handy filters and tags of its own to make common tasks easier.

# Filters

DESCRIPTION	| FILTER AND OUTPUT
----------- | --------
Relative URL<br>Prepend the baseurl value to the input. <br>Useful if your site is hosted at a subpath<br> rather than the root of the domain. | {{ "/assets/style.css" \| relative_url }}<br>/my-baseurl/assets/style.css  
Absolute URL<br>Prepend the url and baseurl value to the input. | {{ "/assets/style.css" \| absolute_url }}<br>http://example.com/my-baseurl/assets/style.css
Date to XML Schema<br>Convert a Date into XML Schema (ISO 8601) format. | {{ site.time \| date_to_xmlschema }}<br>2008-11-07T13:07:54-08:00
Date to RFC-822 Format<br>Convert a Date into the RFC-822 format used for RSS feeds.  | {{ site.time \| date_to_rfc822 }}<br> Mon, 07 Nov 2008 13:07:54 -0800
Date to String<br>Convert a date to short format. | {{ site.time \| date_to_string }}<br>07 Nov 2008
Date to Long String<br>Format a date to long format. | {{ site.time \| date_to_long_string }}<br>07 November 2008
Where<br>Select all the objects in an array where the key has the given value. | {{ site.members \| where:"graduation_year","2014" }} 
Where Expression<br>Select all the objects in an array <br>where the expression is true. Jekyll v3.2.0 & later. | {{ site.members \| where_exp:"item",<br>"item.graduation_year == 2014" }} {{ site.members \| where_exp:"item",<br>"item.graduation_year < 2014" }} {{ site.members \| where_exp:"item",<br>"item.projects contains 'foo'" }}
Group By<br>Group an array's items by a given property. | {{ site.members \| group_by:"graduation_year" }}<br>[{"name"=>"2013", "items"=>[...]},<br>{"name"=>"2014", "items"=>[...]}]
Group By Expression<br>Group an array's items using a Liquid expression. | {{ site.members \| group_by_exp:"item", <br>"item.graduation_year \| truncate: 3, \"\"" }}<br>[{"name"=>"201...", "items"=>[...]},<br>{"name"=>"200...", "items"=>[...]}]  
XML Escape<br>Escape some text for use in XML. | {{ page.content \| xml_escape }}
CGI Escape<br>CGI escape a string for use in a URL. <br>Replaces any special characters with appropriate %XX replacements. | {{ "foo,bar;baz?" \| cgi_escape }}<br>foo%2Cbar%3Bbaz%3F
URI Escape<br>Percent encodes any special characters in a URI. | {{ "http://foo.com/?query=foo, bar \baz?" \| uri_escape }}<br>http://foo.com/?query=foo,%20bar%20%5Cbaz?
Number of Words<br>Count the number of words in some text. | {{ page.content \| number_of_words }}<br>1337
Array to Sentence<br>Convert an array into a sentence. Useful for listing tags.<br>Optional argument for connector. | {{ page.tags \| array_to_sentence_string }}<br>foo, bar, and baz<br>{{ page.tags \| array_to_sentence_string: 'or' }}<br>foo, bar, or baz 
Markdownify<br>Convert a Markdown-formatted string into HTML. | {{ page.excerpt \| markdownify }}<br>
Smartify<br>Convert "quotes" into “smart quotes.” | {{ page.title \| smartify }}
Converting Sass/SCSS<br>Convert a Sass- or SCSS-formatted string into CSS. | {{ some_scss \| scssify }}  {{ some_sass \| sassify }}
Slugify<br>Convert a string into a lowercase URL "slug". <br>See below for options. | {{ "The _config.yml file" \| slugify }} <br> the-config-yml-file<br>{{ "The _config.yml file" \| slugify: 'pretty' }}<br>the-_config.yml-file
Data To JSON<br>Convert Hash or Array to JSON. | {{ site.data.projects \| jsonify }}
Normalize Whitespace<br>Replace any occurrence of whitespace with a single space. | {{ "a \n b" \| normalize_whitespace }}
Sort<br>Sort an array. Optional arguments for hashes:<br> 1. property name 2. nils order (first or last). | {{ page.tags \| sort }}<br>{{ site.posts \| sort: 'author' }}<br>{{ site.pages \| sort: 'title', 'last' }}
Sample<br>Pick a random value from an array. <br>Optional: pick multiple values. | {{ site.pages \| sample }} <br>{{ site.pages \| sample:2 }}
To Integer<br>Convert a string or boolean to integer. | {{ some_var \| to_integer }} 
Array Filters<br>Push, pop, shift, and unshift elements from an Array.<br>These are NON-DESTRUCTIVE, i.e. they do not mutate the array, but rather make a copy and mutate that. | {{ page.tags \| push: 'Spokane' }}<br>['Seattle', 'Tacoma', 'Spokane']<br>{{ page.tags \| pop }}<br>['Seattle']<br>{{ page.tags \| shift }}<br>['Tacoma']<br>{{ page.tags \| unshift: "Olympia" }}<br>['Olympia', 'Seattle', 'Tacoma']<br>
Inspect<br>Convert an object into its String representation for debugging.  | {{ some_var \| inspect }}


**Options** for the `slugify` filter

The `slugify` filter accepts an option, each specifying what to filter. The default is `default`. They are as follows (with what they filter):

*  `none`: no characters
*  `raw`: spaces
*  `default`: spaces and non-alphanumeric characters
*  `pretty`: spaces and non-alphanumeric characters except for `._~!$&'()+,;=@`

# Tags

## Includes

If you have small page snippets that you want to include in multiple places on your site, save the snippets as include files and insert them where required, by using the `include` tag:
```
{% include footer.html %}
```
Jekyll expects all include files to be placed in an `_includes` directory at the root of your source directory. In the above example, this will embed the contents of `_includes/footer.html` into the calling file.

For more advanced information on using includes, see [Includes](http://jekyllrb.com/docs/includes).

## Code snippet highlighting

Jekyll has built in support for syntax highlighting of over 60 languages thanks to [Rouge](http://rouge.jneen.net/). Rouge is the default highlighter in Jekyll 3 and above. To use it in Jekyll 2, set `highlighter` to `rouge` and ensure the `rouge` gem is installed properly.

Alternatively, you can use [Pygments](http://pygments.org/) to highlight your code snippets. To use Pygments, you must have Python installed on your system, have the `pygments.rb` gem installed and set `highlighter` to `pygments` in your site’s configuration file. Pygments supports [over 100 languages](http://pygments.org/languages/) 

To render a code block with syntax highlighting, surround your code as follows:  

```
{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}
```
The argument to the `highlight` tag (`ruby` in the example above) is the language identifier. To find the appropriate identifier to use for the language you want to highlight, look for the “short name” on the [Rouge wiki](https://github.com/jayferd/rouge/wiki/List-of-supported-languages-and-lexers) or the [Pygments’ Lexers page](http://pygments.org/docs/lexers/). 

## Line numbers

There is a second argument to `highlight` called `linenos` that is optional. Including the `linenos` argument will force the highlighted code to include line numbers. For instance, the following code block would include line numbers next to each line:

```
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}
```

## Stylesheets for syntax highlighting

In order for the highlighting to show up, you’ll need to include a highlighting stylesheet. For an example stylesheet you can look at [syntax.css](https://github.com/mojombo/tpw/tree/master/css/syntax.css). These are the same styles as used by GitHub and you are free to use them for your own site. If you use `linenos`, you might want to include an additional CSS class definition for the `.lineno` class in `syntax.css` to distinguish the line numbers from the highlighted code.

## Gist

Use the gist tag to easily embed a GitHub Gist onto your site. This works with public or secret gists:  

```
{% gist parkr/931c1c8d465a04042403 %}
```
You may also optionally specify the filename in the gist to display:  

```
{% gist parkr/931c1c8d465a04042403 jekyll-private-gist.markdown %}
```
To use the `gist` tag, you’ll need to add the [jekyll-gist](https://github.com/jekyll/jekyll-gist) gem to your project.

#Links

##Linking to pages

To link to a post, a page, collection item, or file, the link tag will generate the correct  URL for the path you specify. For example, if you use the link tag to link to mypage.html, even if you change your  style to include the file extension or omit it, the URL formed by the link tag will always be valid.

You must include the file’s original extension when using the link tag. Here are some examples:

```
{{ site.baseurl }}{% link _collection/name-of-document.md %}
{{ site.baseurl }}{% link _posts/2016-07-26-name-of-post.md %}
{{ site.baseurl }}{% link news/index.html %}
{{ site.baseurl }}{% link /assets/files/doc.pdf %}
```
You can also use the link tag to create a link in Markdown as follows:

```
[Link to a document]({{ site.baseurl }}{% link _collection/name-of-document.md %})
[Link to a post]({{ site.baseurl }}{% link _posts/2016-07-26-name-of-post.md %})
[Link to a page]({{ site.baseurl }}{% link news/index.html %})
[Link to a file]({{ site.baseurl }}{% link /assets/files/doc.pdf %})
```
(Including `{{ site.baseurl }}` is optional — it depends on whether you want to preface the page URL with the `baseurl` value.)

The path to the post, page, or collection is defined as the path relative to the root directory (where your config file is) to the file, not the path from your existing page to the other page.

For example, suppose you’re creating a link `page_a.md` (stored in `pages/folder1/folder2`) to `page_b.md` (stored in  `pages/folder1`). Your path in the link would not be `../page_b.html`. Instead, it would be `/pages/folder1/page_b.md`.

If you’re unsure of the path, add `{{ page.path }}` to the page and it will display the path.

One major benefit of using the link tag is `link` validation. If the link doesn’t exist, Jekyll won’t build your site. This is a good thing, as it will alert you to a broken link so you can fix it (rather than allowing you to build and deploy a site with broken links).

Note you cannot add filters to `link` tags. For example, you cannot append a string using Liquid filters, such as `{% link mypage.html | append: "#section1" %}` . To link to sections on a page, you will need to use regular HTML or Markdown linking techniques.

## Linking to posts

If you want like to include a link to a post on your site, the `post_url` tag will generate the correct  URL for the post you specify.

```
{{ site.baseurl }}{% post_url 2010-07-21-name-of-post %}
```
If you organize your posts in subdirectories, you need to include subdirectory path to the post:

```
{{ site.baseurl }}{% post_url /subdir/2010-07-21-name-of-post %}
```
There is no need to include the file extension when using the `post_url` tag.

You can also use this tag to create a link to a post in Markdown as follows:

```
[Name of Link]({{ site.baseurl }}{% post_url 2010-07-21-name-of-post %})
```