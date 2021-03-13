# userstackcfc

A CFML wrapper for the [userstack API](https://userstack.com/documentation).  Use it to lookup and parse user-agent strings.

*Feel free to use the issue tracker to report bugs or suggest improvements!*

## Acknowledgements

This project borrows heavily from the API frameworks built by [jcberquist](https://github.com/jcberquist). Thanks to John for all the inspiration!

## Table of Contents

- [Quick Start](#quick-start)
- [Setup and Authentication](#setup-and-authentication)
- [A Note About HTTPS](#a-note-about-https)
- [`userstackcfc` Reference Manual](#reference-manual)

## Quick Start

Use of the component .

```cfc
userstack = new path.to.userstackcfc.userstack( access_key = 'xxx' );

ua = "Mozilla/5.0 (iPad; U; CPU OS 3_2_1 like Mac OS X; en-us) AppleWebKit/531.21.10 (KHTML, like Gecko) Mobile/7B405";

result = userstack.detect( ua );

writeDump( var='#result#' );
```

### Setup and Authentication

To get started with the Userstack API, you'll need an [Access Key](https://userstack.com/documentation#access_keys).

Once you have this, you can provide it to this wrapper manually when creating the component, as in the Quick Start example above, or via an environment variables named `USERSTACK_ACCESS_KEY`, which will get picked up automatically. This latter approach is generally preferable, as it keeps hardcoded credentials out of your codebase.

### A Note About HTTPS

For reasons I don't understand, the secure endpoint for the API [is restricted to paid plans](https://userstack.com/documentation#https). This wrapper implements the HTTPS endpoint as the default. Consequently, if you are on the free tier, you'll need to manually override the `baseurl` when you first init the component, like this:

```cfc
  userstack new path.to.userstackcfc.userstack(
    baseUrl = 'http://api.userstack.com',
    access_key = 'xxx'
  );
```

## Reference Manual

#### `detect( required string ua,  string fields,  string callback,  string output )`

Lookup a single user-agent. The parameter `ua` specifies the User-Agent string to be looked up. The parameter `fields` [optional] can be used to specify API response field(s). *[Further docs](https://userstack.com/documentation#single_lookup)*

---
