My personal blog.

## Development instructions
1. Incremental build:
```
bundle exec jekyll serve --incremental
```

2. Copy built files to `docs/`:
```
rm -rf ../docs/*
cp -rf _site/* ../docs
```
