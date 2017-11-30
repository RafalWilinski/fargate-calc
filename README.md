# AWS Fargate Pricing Calculator

Simple Vue.js based app for calculating price of AWS Fargate containers.

Based on https://aws.amazon.com/fargate/pricing/

## Build Setup

``` bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for production and view the bundle analyzer report
npm run build --report
```

For a detailed explanation on how things work, check out the [guide](http://vuejs-templates.github.io/webpack/) and [docs for vue-loader](http://vuejs.github.io/vue-loader).

## Deployment

Use https://github.com/klaemo/s3-website

```bash
npm run build && s3-website deploy ./dist
```

