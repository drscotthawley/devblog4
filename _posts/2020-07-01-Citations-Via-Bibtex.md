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


Hopefully what just happened above is that two citation markings were generated, and these then point to the References section at the end of this post where the full citations are printed out, using the citation format of my choice.


## Drawing from the Bibliography 

To get the full citation info, we will draw from the sample BibTeX file [references.bib](../_bibliography/references.bib), which lives in a new directory we created called `_bibliography/`, and looks like this:

```bibtex
@conference{signaltrain,
  title = {Profiling Audio Compressors with Deep Neural Networks},
  author = {Hawley, Scott and Colburn, Benjamin and Mimilakis, Stylianos Ioannis},
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

(**NOTE:** jekyll-scholar hates the `url`, `howpublished` and `note` fields that many of us are now accustomed to.  Not only will it not recognize them, it will throw an error and abort the build if any of these are encountered.)


At the end of your post, you signal the creation of the full list of references by using the Liquid tag

```liquid
{% raw %}{% bibliography --cited %}{% endraw %}
```

...so I'll put that at the very bottom of this file.  (Currently that'll generate an error, because we haven't enabled jekyll-scholar yet, but we'll do that below.)   The `--cited` means that it'll only include those references that are actually used in your post -- no need to include hundreds of references from your BibTeX database that aren't used!


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




# References

{% bibliography --cited %}
