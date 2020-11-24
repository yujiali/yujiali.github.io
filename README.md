# Personal website based on jekyll

[View the website](https://yujiali.github.io/).

## Build

Building site using default configs:

```bash
jekyll build
```

Then serve the website locally to debug issues:
```bash
jekyll serve
```

If there are special configs, build site using

```bash
jekyll build --config <config_file>.yml -d <destination>
```

## Deployment

Deployment on github does not require any special treatment, just push the changes through would be sufficient.

In order to deploy to other sites that only support static content, copy the generated `_site` (or `<destination>` if a special config was used) folder to the destination.
