My personal blog.

## Development instructions
1. Incremental build:
```
bundle exec jekyll serve --incremental
```

## Deployment instructions
1. Build with `JEKYLL_ENV="production"`:
``` 
JEKYLL_ENV="production" bundle exec jekyll build
```
2. Copy built files to `docs/`:
```
rm -rf ../docs/*
cp -rf _site/* ../docs
```
