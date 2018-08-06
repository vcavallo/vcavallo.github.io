---
layout: post
title: bash-script-used-for-jekyll-mass-rename
---

given a bunch of files that look roughly this (with the `original_draft_date`
part being most important):

```
# 2018-08-06-post-title.md

---
layout: post
title: something or other
original_draft_date: 2017-01-01
--

some post content...
```

I used the following script

```
FILES=2018-08-06*.md
for f in $FILES
do
  DATE=$(grep 'original_draft_date: ' $f | cut -d" " -f2)
  mv $f ${f//2018-08-06/$DATE}
done
```

This collected all files starting with `2018-08-06` into a variable. then, looping over
those files, it got the `original_draft_date` value and stored it off into a
variable.

It did this by grepping for `original_draft_date: ` and using `cut` to get the bit
_after the space only_. (grep would output `original_draft_date: 2017-01-01`) This was key because otherwise I was getting the entire
match (including `original_draft_date`). 

There were some other possible
approaches using `sed`, but this was easier (and I never quite
learned/remembered `sed`'s syntax, even though its so close to a lot of vim).

Once I had the date, I could use `mv` to
rename the files replacing the old date with the new one from the `$DATE`
variable. Looking at it a little closer:  Assuming the original filename is
`2018-08-06-post-title.md` and the value stored in `$DATE` is `2017-01-01`,
then `mv $f ${f//2018-08-06/$DATE}` evaluates to: `mv 2018-08-06-post-title.md
2017-01-01-post-title.md` using [substring search and
replace](http://wiki.bash-hackers.org/syntax/pe#search_and_replace) here: `${f//2018-08-06/$DATE}`.
