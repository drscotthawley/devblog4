---
title: "Citations in Fastpages via BibTeX and jekyll-scholar"
description: Supporting scholarly blogging by drawing references from your database.
layout: post
toc: true
comments: true
image:
hide: false
search_exclude: false
---

## How to Cite 

Since this is my own post, I'll take the liberty of citing my own papers ;-), namely the first SignalTrain paper{% cite signaltrain %} and the new one by Billy Mitchell{% cite billy_signaltrain2 %}.  Instead of using the LaTeX format of {% raw %}\cite{ \<whatever> }{% endraw %}, we use the Liquid format of {% raw  %}{% cite \<whatever> %}{% endraw %}.


Hopefully what just happened above is that two citation markings were generated, and these point to the References section at the end of this post where the full citations are printed out using the citation format of my choice.


## Drawing from the Bibliography 

In the main blog directory, create a new directory called `_bibliography`, and place your BibTeX file there as [references.bib](../_bibliography/references.bib).  In the case of this post, the references file looks like this:

```bibtex
@conference{signaltrain,
  title = {Profiling Audio Compressors with Deep Neural Networks},
  author = {Hawley, Scott H. and Colburn, Benjamin and Mimilakis, Stylianos Ioannis},
  booktitle = {Audio Engineering Society Convention 147},
  month = {Oct},
  year = {2019},
}               

@article{billy_signaltrain2, 
  title={Exploring Quality and Generalizability in Parameterized Neural Audio Effects},
  author={William Mitchell and Scott H. Hawley},
  journal={ArXiv},  
  year={2020},
  volume={abs/2006.05584} 
} 
```

**NOTES:**

1. This is one references file for your entire blog. The great thing is that all your notebooks, all your Markdown posts, will draw from this same one file, which could be hundreds of references long, and jekyll-scholar will only include the ones you need for each post. 
2. jekyll-scholar hates the `url`, `howpublished` and `note` fields that many of us are now accustomed to.  Not only will it not recognize them, it will throw an error and abort the build if any of these are encountered.  I'm not yet sure how to get links into the references, but [watch this space](https://github.com/inukshuk/jekyll-scholar/issues/308).


Finally, the end of your post, you signal the creation of the full list of references by using the Liquid tag

```liquid
{% raw %}{% bibliography --cited %}{% endraw %}
```

...so I'll put that at the very bottom of this file.  (Currently that'll generate an error, because we haven't enabled jekyll-scholar yet, but we'll do that next.)   The `--cited` means that it'll only include those references that are actually used in your post -- i.e., so it won't post hundreds of references from your BibTeX database that aren't being cited in this post!


## Enabling Jekyll-Scholar


To enable jekyll-scholar, all we need to do is make the following two changes, and perhaps a third.  

1. In `_config.yml`, add "` - jekyll-scholar`" to the list of `plugins:`.

2. Edit the `Gemfile` to include `gem 'jekyll-scholar'` where the other plugins are listed. 

3. Optional: The defaut citation format is "apa".  If you want to change that, you can specify a different [CSL](https://citationstyles.org/) file, only without the .csl.  In my case, I found the file `physical-review-d.csl`, copied it into my main blog directory, and then added the following to my `_config.yml` file:

```yaml
scholar:
  style: physical-review-d
```
...in order to render the citation style you see below (as well as the use of numbered brackets above for the citation markers).   

By the way, did you notice what we just did with the citation format?  The convenience of this BibTeX/jekyll-scholar approach is that instead of having to manually edit full references on each individual page -- say, you wanted to change citation formats (or alternatively, update certain information about one paper that appears in multiple posts) -- now you only change **one line** in `_config.yml` (or correct the reference in one spot in `references.bib`) and the system "builds out" the change "everywhere. "

Happy blogging! 


# References

{% bibliography --cited %}

