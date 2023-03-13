---
head:
  - - meta
    - name: description
      content: Coolify - Applications - Docker
  - - meta
    - name: keywords
      content: applications docker coollabs coolify 
  - - meta
    - name: twitter:card
      content: summary_large_image
  - - meta
    - name: twitter:site
      content: '@andrasbacsai'
  - - meta
    - name: twitter:title
      content: Coolify
  - - meta
    - name: twitter:description
      content: An open-source & self-hostable Heroku / Netlify alternative.
  - - meta
    - name: twitter:image
      content: https://cdn.coollabs.io/assets/coollabs/og-image-applications.png
  - - meta
    - property: og:type
      content: website
  - - meta
    - property: og:url
      content: https://coolify.io
  - - meta
    - property: og:title
      content: Coolify
  - - meta
    - property: og:description
      content: An open-source & self-hostable Heroku / Netlify alternative.
  - - meta
    - property: og:site_name
      content: Coolify
  - - meta
    - property: og:image
      content: https://cdn.coollabs.io/assets/coollabs/og-image-applications.png
---
# Docker
The Docker build pack is a powerful one. You can use your Dockerfile to build & serve your applications. It means you can deploy any unsupported (natively with build packs) applications, services, anything, where a simple Docker file is enough!

## Sample with [Baserow](https://baserow.io/)

[docker tutorial](https://baserow.io/docs/installation%2Finstall-with-docker)

I choose Baserow as an example application because the config can be tweaked to allow for different ways of running the application. You can for example try using a postgres and redis deployed with coolify and pass their urls as variables to Baserow application.

- Create a repository on GitHub where you will keep only the Dockerfile.
- Create and push a simple dockerfile, than only mentions the image you want to use, like so:

```docker
FROM baserow/baserow:1.10.2
```

- Create an application in Coolify:
   1. Click on `Create New Resource` button and select `Application`
   2. Select a GitSource that has access to the repository or specify a Public Repository URL.
   :::tip
   With Public Repository, you won't get the auto-commit builds. You need to initiate rebuild manually.
   :::
   3. Select `Docker` as build pack.
   4. Make sure the `port` field is set, otherwise Coolify won't know which port to expose (for example in the case of baserow it will be 80 instead of 3000).
   5. Add any env variables that are required to start the container in the top right `Secrets` panel - in case of Baserow the only thing you need to add is `BASEROW_PUBLIC_URL` which should correspond to the url you've set for the application.
   6. If your application needs volumes mounted / to persist data between runs safely add persistent storage in the bottom right `Persistent Storage` panel. In the case of Baserow you need to add only `/baserow/data` as a volume.
   7. Optionally switch on debug logs - should be the law option in the app settings panel.
- Deploy your application.
- Enjoy.
