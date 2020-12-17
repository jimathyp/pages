# Jekyll

https://jekyllrb.com/


## Code blocks

https://jekyllrb.com/docs/liquid/tags/

eg. syntax highlighting


{% highlight ruby %}
def foo
  puts 'foo'
end
{% endhighlight %}




## Escaping  Liquid templates

https://stackoverflow.com/questions/3426182/how-to-escape-liquid-template-tags

Can use 
a block


{% raw  %}
{% this %}
{% endraw %}



## Includes

Files to be included are in the `_includes` folder.

{% raw  %}
{% include footer.html %}
{% endraw %}




## Variables

https://jekyllrb.com/docs/variables/

`site.pages` a list of all pages
