- github pages needs `master` to be the site-hosting branch for User pages.
- github pages doesn't allow custom themes to be built on their end, so need to build locally:
- `source` branch should be considered the "master" branch as far as working goes. work there, generate a new `_site` folder.
- untested, but I believe this is the new process for deploying:

```
git subtree split --prefix _site/ master
git push -f origin master:master
```
