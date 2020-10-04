# minhdq99hp.github.io

## Setup
```
sudo apt-get install ruby-full build-essential zlib1g-dev
```

```
echo '# Install Ruby Gems to ~/gems' >> ~/.bashrc
echo 'export GEM_HOME="$HOME/gems"' >> ~/.bashrc
echo 'export PATH="$HOME/gems/bin:$PATH"' >> ~/.bashrc
source ~/.bashrc
```

```
gem install jekyll bundler
```

Install additional gems:
```
bundle install
```

## Run
```
bundle exec jekyll serve
```

Build jekyll
```
bundle exec jekyll build --incremental
```
