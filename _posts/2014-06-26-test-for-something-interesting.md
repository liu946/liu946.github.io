---
layout: bsdef
title: test for something interesting
---

<div style="margin:30px;">
<div class="page-header">
  <h1>Test<br><small>test for something cool!</small></h1>
</div>
<div>
<h3>
<h2>include</h2>
<br>
{% include code.html call="test" %}
<hr>
<h2>code
</h2>
<br>
{% highlight ruby linenos %}
def foo
  puts 'foo'
end
{% endhighlight %}
<hr>
<h2>URL to a artical
</h2>
<br>
hello-world
{% post_url 2014-06-25-hello-world %}
[hello-world]
({% post_url 2014-06-25-hello-world %})
<hr>
<h2>gist
</h2>
<br>
{% gist liu946/b216f39523f71d2e436e %}


</h3>
</div>
</div>