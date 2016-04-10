# Vagrant Box for Github Pages

## Scripts

The Vagrant box includes a basic set of scripts based on Github's
[conventions](https://github.com/github/scripts-to-rule-them-all).

## Usage

1. Run `vagrant up` and `vagrant ssh` into the box (or `./vssh`)
2. Run `script/new` to generate a new [Jekyll](https://jekyllrb.com) site, or copy your favorite template on top
3. Add your domain to [CNAME](CNAME)
4. Edit your github repo address at [script/settings](script/settings)
5. Run `script/cibuild` to generate the site
6. Run `script/deploy` override the _gh-pages_ branch with the newly generated site