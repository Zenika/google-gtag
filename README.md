# @zenika/nuxtjs-google-gtag

This is a fork of [@nuxtjs/google-gtag](https://github.com/nuxt-community/google-gtag).

With the original lib, the gtag script tag is added through the nuxt config and rendered on the server-side. This is problematic because it means gtag is unconditionally run on the client, even though it adds a cookie on the visitor's computer without their consent, which is illegal in the European Union.

With this fork, the client-side application can control when the gtag script is added to the page, enabling the application developper to correctly implement the law.

To begin tracking, typically after the visitor has given their consent, call `this.$enableGtagTracking()` in any component.

⚠️ No tracking will take place if `this.$enableGtagTracking()` is not called!

The rest of the lib behavior remains intact. `this.$gtag(...)` can even be called before `this.$enableGtagTracking()` without errors, and without loss of events.

The original documentation follows.

# @nuxtjs/google-gtag
[![npm (scoped with tag)](https://img.shields.io/npm/v/@nuxtjs/google-gtag/latest.svg?style=flat-square)](https://npmjs.com/package/@nuxtjs/google-gtag)
[![npm](https://img.shields.io/npm/dt/@nuxtjs/google-gtag.svg?style=flat-square)](https://npmjs.com/package/@nuxtjs/google-gtag)
[![CircleCI](https://img.shields.io/circleci/project/github/https://github.com/nuxt-community/google-gtag.svg?style=flat-square)](https://circleci.com/gh/https://github.com/nuxt-community/google-gtag)
[![Codecov](https://img.shields.io/codecov/c/github/https://github.com/nuxt-community/google-gtag.svg?style=flat-square)](https://codecov.io/gh/https://github.com/nuxt-community/google-gtag)
[![Dependencies](https://david-dm.org/https://github.com/nuxt-community/google-gtag/status.svg?style=flat-square)](https://david-dm.org/https://github.com/nuxt-community/google-gtag)
[![js-standard-style](https://img.shields.io/badge/code_style-standard-brightgreen.svg?style=flat-square)](http://standardjs.com)

> Google official gtagjs for Nuxt.js

[📖 **Release Notes**](./CHANGELOG.md)

## Features

The module includes Google `googletagmanager.com/gtag/js` into your project and enables it with config you pass in as options.

* Check the official reference [gtag](https://developers.google.com/analytics/devguides/collection/gtagjs/)

## Setup
- Add `@nuxtjs/google-gtag` dependency using yarn or npm to your project
- Add `@nuxtjs/google-gtag` to `modules` section of `nuxt.config.js`

```js
{
  modules: [
    // Simple usage
    '@nuxtjs/google-gtag',

    // With options
    ['@nuxtjs/google-gtag', { /* module options */ }],    
 ]
  
 // example config
 'google-gtag':{
   id: 'UA-XXXX-XX', // required
   config:{
     // this are the config options for `gtag
     // check out official docs: https://developers.google.com/analytics/devguides/collection/gtagjs/
     anonymize_ip: true, // anonymize IP 
     send_page_view: false, // might be necessary to avoid duplicated page track on page reload
     linker:{
       domains:['domain.com','domain.org']
     }
   },
   debug: true, // enable to track in dev mode
   disableAutoPageTrack: false, // disable if you don't want to track each page route with router.afterEach(...)
   // optional you can add more configuration like [AdWords](https://developers.google.com/adwords-remarketing-tag/#configuring_the_global_site_tag_for_multiple_accounts)
   additionalAccounts:[{
     id: 'AW-XXXX-XX', // required if you are adding additional accounts
     config:{
       send_page_view:false // optional configurations
     }
   }]
  }
}
```
## Usage

```
  this.$gtag('event', 'your_event', { /* track something awesome */})
```
See official docs:
* [gtagjs](https://developers.google.com/analytics/devguides/collection/gtagjs/)
* [adwords](https://developers.google.com/adwords-remarketing-tag/#configuring_the_global_site_tag_for_multiple_accounts)

## Check functionalities

Install [`Google Tag Assistant`](https://chrome.google.com/webstore/detail/tag-assistant-by-google/kejbdjndbnbjgmefkgdddjlbokphdefk?hl=en) and see if your page is being tracked.

## Development

- Clone this repository
- Install dependencies using `yarn install` or `npm install`
- Start development server using `npm run dev`

## License

[MIT License](./LICENSE)

Copyright (c) Dominic Garms <djgarms@gmail.com>
