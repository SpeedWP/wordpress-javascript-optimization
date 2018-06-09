[![Build Status](https://travis-ci.org/o10n-x/wordpress-javascript-optimization.svg?branch=master)](https://travis-ci.org/o10n-x/wordpress-javascript-optimization) ![Version](https://img.shields.io/github/release/o10n-x/wordpress-javascript-optimization.svg)

# WordPress Javascript Optimization

Advanced Javascript optimization toolkit. Minify, concat/merge, async loading, advanced editor, ES Lint, UglifyJS (professional), beautifier and more.

* [Documentation](https://github.com/o10n-x/wordpress-javascript-optimization/tree/master/docs)
* [Description](https://github.com/o10n-x/wordpress-javascript-optimization#description)
* [Version history (Changelog)](https://github.com/o10n-x/wordpress-javascript-optimization/releases)
## Installation

![Github Updater](https://github.com/afragen/github-updater/raw/develop/assets/GitHub_Updater_logo_small.png)

This plugin can be installed and updated using [Github Updater](https://github.com/afragen/github-updater) ([installation instructions](https://github.com/afragen/github-updater/wiki/Installation))

<details/>
  <summary>Installation instructions</summary>

### Step 1: Install Github Updater and first optimization plugin

Installing and updating the plugins is possible using Github Updater. It is easy to install one of the plugins. You simply need to download the Github Updater plugin ([zip file](https://github.com/afragen/github-updater/archive/develop.zip)), install it from the WordPress plugin admin panel and copy the Github URL of the plugin into the Github Updater installer.

![image](https://user-images.githubusercontent.com/8843669/39889846-46158cc2-5499-11e8-824d-720020f758db.png)

### Step 2: Install other optimization plugins with a single click

A recent update of all plugins contains a easy single click install button.

![image](https://user-images.githubusercontent.com/8843669/39661507-cc1eac5e-5052-11e8-8fba-33c0cc959b07.png)
</details>

## Description

This plugin is a toolkit for professional Javascript optimization.

The plugin provides in a complete solution for code optimization and delivery optimization (minify, concat/merge (with groups), async loading, timed execution and more).

### Multiple minifiers and custom minifier

The plugin provides the option to minify Javascript code using multiple Javascript minifiers including [JSMin](https://github.com/mrclay/jsmin-php) (PHP), [Google Closure Compiler API](https://github.com/google/closure-compiler) and the option to use a custom minifier using a WordPress filter that enables to use any solution, including a Amazon Lambda or Google Cloud function with Node.js based Javascript optimization software.

![Javascript Code Optimization](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/google-closure-compiler-optimization.png)

#### Custom minifier

<details/>
  <summary>Show custom minifier example</summary>

```php
/* Custom Javascript minifier */
add_filter('o10n_js_custom_minify', function ($JS) {

    // apply javascript optimization
    exec('/node /path/to/optimize-js.js /tmp/js-source.js');
    $minified = file_get_contents('/tmp/output.js');

    // alternative
    $minified = JSCompressor::minify($JS);

    return $minified;

});
```
</details>

### Async loading and timed download and/or execution

The plugin provides many unique innovations including timed script downloading and/or execution based on `requestAnimationFrame` with frame target, `requestIdleCallback`, element scrolled into view or a Media Query.

The plugin enables to download and/or execute scripts based on a Media Query or element scrolled into viewport enabling to optimize Javascript loading for individual devices (e.g. save +500kb of scripts on mobile devices).

![Async Load Config Filter](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/async-load-config.png)
![Timed Javascript Exec](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/timed-exec.png)

### Service Worker Push

The plugin provides a unique innovation called **Service Worker Push**. It is an alternative for HTTP/2 Server Push + Cache-Digest with better performance and better efficiency.

Cache-Digest is not yet an official supported feature. HTTP/2 Server Push without Cache-Digest causes a lot of overhead and has almost no performance advantage.

- Performance study: https://calendar.perfplanet.com/2016/cache-digests-http2-server-push/
- Google engineer: https://jakearchibald.com/2017/h2-push-tougher-than-i-thought/

Cache-Digest calculation for thousands of assets causes overhead. Service Worker Push has direct access to the browser cache storage and is therefor able to support millions of cached assets without performance loss.

Service Worker Push uses PHP method `\O10n\attach_preload()` to attach assets such as images, stylesheets and scripts to a page which are then exposed to a Service Worker using a HTTP header. The Service Worker is then able to preload assets intelligently on the basis of a page URL.

```php
/* Attach assets to page for smart preloading in the Service Worker */
add_action('init', function() {

    if (function_exists('O10n\attach_preload')) {

        // attach single asset to page
        \O10n\attach_preload('/path/to/image.jpg');

        // attach multiple assets to page
        \O10n\attach_preload(array('/path/to/image.jpg', 'https://cdn.google.com/script.js', '/path/to/stylesheet.css'));

    }
});
```

The Service Worker Optimization plugin ([PWA Optimization](https://github.com/o10n-x/wordpress-pwa-optimization)) provides an option to preload pages for offline availability and an option to start preloading a page on mouse down. Service Worker Push enables to automatically load all essential assets of a page on the basis of page URLs which makes it easy to make a full website available offline, or to provide an instant navigation experience for websites with many unique assets per page.

With the mouse-down preload option + Service Worker Push for CSS, the stylesheets of a page would start loading in the background as soon as a user touches a link.

### Localstorage

The plugin provides the option to cache stylesheets using localStorage with a HTTP `HEAD` based background update. LocalStorage has proven to be exceptionally fast for loading CSS, much faster than browser cache.

![localStorage Javascript](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/localstorage.png)

### External Script Proxy

The plugin provides a unique innovation to capture and proxy external script injected scripts to pass the [Leverage browser caching](https://developers.google.com/speed/docs/insights/LeverageBrowserCaching) rule from Google PageSpeed Insights.

![Script Proxy](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/proxy.png)

With debug modus enabled, the browser console will show detailed information about the Javascript loading and execution process including a [Performance API](https://developer.mozilla.org/nl/docs/Web/API/Performance) result for an insight in the Javascript loading performance of any given configuration.

![Browser Console performance debug](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/console-performance.png)

### Javascript Editor

The plugin contains an advanced Javascript editor with ES Lint, UglifyJS code optimization and a Javascript beautifier. The editor can be personalized with more than 30 themes.

![Advanced Javascript Editor](https://github.com/o10n-x/wordpress-javascript-optimization/blob/master/docs/images/js-editor.png)

Additional features can be requested on the [Github forum](https://github.com/o10n-x/wordpress-javascript-optimization/issues).

## WordPress WPO Collection

This plugin is part of a Website Performance Optimization collection that include [CSS](https://github.com/o10n-x/wordpress-css-optimization), [HTML](https://github.com/o10n-x/wordpress-html-optimization), [Web Font](https://github.com/o10n-x/wordpress-font-optimization), [HTTP/2](https://github.com/o10n-x/wordpress-http2-optimization), [Progressive Web App (Service Worker)](https://github.com/o10n-x/wordpress-pwa-optimization) and [Security Header](https://github.com/o10n-x/wordpress-security-header-optimization) optimization. 

The WPO optimization plugins provide in all essential tools that enable to achieve perfect [Google Lighthouse Test](https://developers.google.com/web/tools/lighthouse/) scores and to validate a website as [Google PWA](https://developers.google.com/web/progressive-web-apps/), an important ranking factor for Google's [Speed Update](https://searchengineland.com/google-speed-update-page-speed-will-become-ranking-factor-mobile-search-289904) (July 2018).

![Google Lighthouse Perfect Performance Scores](https://github.com/o10n-x/wordpress-css-optimization/blob/master/docs/images/google-lighthouse-pwa-validation.jpg)

The WPO optimization plugins are designed to work together with single plugin performance. The plugins provide the latest optimization technologies and many unique innovations.

### JSON shema configuration

The WPO optimization plugins are based on JSON schema based configuration that enables full control of the optimization using JSON. This provides several great advantages for website performance optimization.

Read more about [JSON schemas](https://github.com/o10n-x/wordpress-o10n-core/tree/master/schemas).

## Google PageSpeed vs Google Lighthouse Scores

While a Google PageSpeed 100 score is still of value, websites with a high Google PageSpeed score may score very bad in Google's new [Lighthouse performance test](https://developers.google.com/web/tools/lighthouse/). 

The following scores are for the same site. It shows that a perfect Google PageSpeed score does not correlate to a high Google Lighthouse performance score.

![Perfect Google PageSpeed 100 Score](https://github.com/o10n-x/wordpress-css-optimization/blob/master/docs/images/google-pagespeed-100.png) ![Google Lighthouse Critical Performance Score](https://github.com/o10n-x/wordpress-css-optimization/blob/master/docs/images/lighthouse-performance-15.png)

### Google PageSpeed score is outdated

For the open web to have a chance of survival in a mobile era it needs to compete with and win from native mobile apps. Google is dependent on the open web for it's advertising revenue. Google therefor seeks a way to secure the open web and the main objective is to rapidly enhance the quality of the open web to meet the standards of native mobile apps.

For SEO it is therefor simple: websites will need to meet the standards set by the [Google Lighthouse Test](https://developers.google.com/web/tools/lighthouse/) (or Google's future new tests). A website with perfect scores will be preferred in search over low performance websites. The officially announced [Google Speed Update](https://searchengineland.com/google-speed-update-page-speed-will-become-ranking-factor-mobile-search-289904) (July 2018) shows that Google is going as far as it can to drive people to enhance the quality to ultra high levels, to meet the quality of, and hopefully beat native mobile apps.

A perfect Google Lighthouse Score includes validation of a website as a [Progressive Web App (PWA)](https://developers.google.com/web/progressive-web-apps/).

Google offers another new website performance test that is much tougher than the Google PageSpeed score. It is based on a AI neural network and it can be accessed on https://testmysite.thinkwithgoogle.com
