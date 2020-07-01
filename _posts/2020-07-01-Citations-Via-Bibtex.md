---
title: "Citations in Fastpages via BibTex and jekyll-scholar"
description: Supporting scholarly blogging by drawing references from your database.
layout: post
toc: true
comments: true
image:
hide: false
search_exclude: false
---

## How to Cite 

Since this is my post, I'll take the liberty of citing my own papers ;-), namely the first SignalTrain paper {% cite signaltrain %} and the second one by Billy Mitchell {% cite billy_signaltrain2 %}.  Instead of using the LaTeX format of {% raw %}`\cite{ <whatever> }`{% endraw %}, we use the Liquid format of {% raw  %}`{% cite <whatever> %}`{% endraw %}.



Hopefully what just happened above is that two citation markings were generated, and these then point to the References section at the end of this post where the full citations are printed out, using the citation format of my choice.


## Drawing from the Bibliography 

To get the full citation info, we will draw from the sample BibTex file [bibliography.bib](bibliography.bib), which looks like this:

```bibtex
@conference{signaltrain,
  title = {Profiling Audio Compressors with Deep Neural Networks},
  author = {Hawley, Scott and Colburn, Benjamin and Mimilakis, Stylianos Ioannis},
  booktitle = {Audio Engineering Society Convention 147},
  month = {Oct},
  year = {2019},
  url = {http://www.aes.org/e-lib/browse.cfm?elib=20595}
}               

@article{billy_signaltrain2, 
  title={Exploring Quality and Generalizability in Parameterized Neural Audio Effects},
  author={William Mitchell and Scott H. Hawley},
  journal={ArXiv},  
  year={2020},
  volume={abs/2006.05584} 
  url = {https://arxiv.org/abs/2006.05584}
} 
```

**NOTE #1:** You might get the impression from the jekyll-scholar docs that you can name this file anything you want.  Good luck with that!  I started this blog entry using the file `references.bib`.  The problem is that the Liquid tag you need (see next section) refers to `bibliography`.  

**NOTE #2:** jekyll-scholar hates the `url` BibTeX tag.  Not will it not recognize it, it will throw and error and fail if the `url` tag is encountered! ??



## Enabling Jekyll-Scholar

Currently `bibliography.bib` lives in the `_posts/` directory, but maybe there's a better place to store it.  [The instructions for jekyll-scholar](https://github.com/inukshuk/jekyll-scholar) say that it scans for any `.bib` file anywhere in the blog, so this may be more a matter of establishing a convention.   [User rahuketu86 suggested](https://forums.fast.ai/t/how-to-include-citation-in-nbdev-exported-html/62462/8?u=drscotthawley) creating a `_bibliography` directory and putting the references there.



The .bib file will then get converted to a `.html` file, so in my case it'll be `bibliography.html`, and this can then be imported via a Liquid tag: 

```liquid
{% raw %}{% bibliography --cited %}{% endraw %}
```

...so I'll put that at the very bottom of this file.   Currently that'll generate a Liquid Syntax Error, `Unknown tag 'references'`, because we haven't enabled jekyll-scholar yet.   The `--cited` means that it'll only include those reference that are actually used in your post -- no need to include hundreds of references from your BibTeX database that aren't used!



To enable jekyll-scholar, Hamel says we don't need to do anything installation-wise, so I hope that all I need to do is make the following two changes in `_config.yml`:

1. Add "` - jekyll-scholar`" to the list of `plugins:`.

2. Elsewhere in the file, specify a citation format e.g., 

```yaml
scholar:
  style: mla
```









# References

{% bibliography --cited %}

