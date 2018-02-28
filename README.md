# Hands Off My TLD
If you run local development environment with your own TLD (**.dev**, **.local**, **etc**) then you have run into times where the browser trumps your local domain by routing it, or worse, by searching with it.

**homtld** is a *Safari Extension* that forces the [Smart Search](https://support.apple.com/guide/safari/smart-search-field-ibrw74269f2c/mac) to treat URIs ending in **your** protected top level domain(s) like the universally accepted ones *(ie. .com)*.

### Background
We have all gotten too lazy to type `http://` and so every major browser has some helper that decides when to search or retrieve a URL. It makes it so that `github.com` takes you to their site but `Maritime law` goes to your search engine. That's great when the browser recognizes your TLD. However, my preferred local (**.odd**) isn't recognized so I kept searching the google for `client1.odd`. Granted, it's only a minor annoyance but this Monday was the *wrong* day.

### Installation
Waiting on Apple to have this up in the [Safari Extensions Gallery](https://safari-extensions.apple.com/).

Until then, you can install manually by:
1) Clicking [here](https://github.com/lilolbear/Hands-Off-My-TLD/raw/master/Hands-off-my-TLD.safariextz) to download the **.safariextz** file.
2) Find and click the file to get Safari to open it.
3) Decide if you want to **Trust** it or wait until it's in the aforementioned Extensions Gallery.
4) Assuming that you trusted it, then you can configure it.

### Configuration
option | default | description
--- | --- | ---
Protected TLDs (comma separated)  | `.odd, .local` | comma separated list of suffixes (TDLs) that the extension will look for.
Use SSL | `false` | whether to prepend `http://` or `https://`
Silence Alarm | `true` | mostly for debugging, this does a javascript alert when it captures a TLD

### Reference
##### Tech
Works by intercepting the [SafariBeforeSearchEvent](https://developer.apple.com/documentation/safariextensions/safaribeforesearchevent) and examining the query string to see if it ends *(ignoring whitespace)* in a protected TLD. If it finds one of these  protected strings then it adds `http://` or `https://` *(if you pick 'Use SSL')* to the start of the query. Otherwise it just gets out of the way.

> If you're concerned about security, it doesn't have access to anything. Just grabs the query and prepends to it.

##### My Local Development Environment
MacOS High Sierra (10.13) doing a wildcard custom domain name (**\*.odd**) using:
* [Apache](https://www.apache.org/) - because it's conveniently preinstalled on macOS
* [dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) - awesome tool to give me wildcard subdomain names
* ... and a bunch more that are irrelevant to this project ([github](http://github.com), [homebrew](https://brew.sh), [mysql](https://www.mysql.com/), [etc](http://atom.io), [etc](https://www.npmjs.com), [etc](http://gulp.js))

For those who are unfamiliar, this setup allows me to define **\*.odd** domains to all route to 127.0.0.1 and end up in appropriate subfolders within my [DocumentRoot](https://httpd.apache.org/docs/2.4/mod/mod_vhost_alias.html):

url | destination
--- | ---
[client1.odd]() | `~/Sites/client1`
[client2.odd]() | `~/Sites/client2`
[home.odd]() | `~/Sites/home`

I like to use **\*.odd** as my development domain because I despise **.test** and **.dev** is a [hot mess](https://medium.engineering/use-a-dev-domain-not-anymore-95219778e6fd) since being bought.

### Todos

 - Port over to Chrome (*and Firefox?*)
 - Get some Pizza

License
----

MIT
