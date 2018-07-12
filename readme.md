# working

- `$ jekyll draft [NAME]`
- `$ jekyll serve --draft` shows drafts as published. (note, excepts will not work this way)

# deploying
- github pages needs `master` to be the site-hosting branch for User pages.
- github pages doesn't allow custom themes to be built on their end, so need to build locally:
- `source` branch should be considered the "master" branch as far as working goes. work there, generate a new `_site` folder with `jekyll build`.
- add and commit new `_site`
- deploy with: `git subtree push --prefix _site origin master` - or with `bin/deploy`
