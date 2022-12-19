# Tom Stesco - personal projects website

Personal website and blog built using Jekyll and hosted on github-pages, [visit the site here](https://tomstesco.com).

Tested with:
- Node v8.0.0
- NPM v5.0.0
- Bundler v1.16.0
- Gem v2.7.1

If you're using NVM, this will get you to the right Node/NPM versions:
```$bash
nvm use v8.0.0
```
 
You will need to intall some additional tools:
```$bash
sudo apt install ruby-dev
npm install gulp -g
sudo gem install bundler
# if things arent working try: rm Gemfile.lock before bundle install
bundle install
npm install
```

To run:
```$bash
bundle exec gulp
```
