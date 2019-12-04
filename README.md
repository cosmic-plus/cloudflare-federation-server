**cloudflare-federation-server /**
[Readme](https://cosmic.plus/#view:cloudflare-federation-server)
• [Contributing](https://cosmic.plus/#view:cloudflare-federation-server/CONTRIBUTING)
• [Changelog](https://cosmic.plus/#view:cloudflare-federation-server/CHANGELOG)

# Readme

![Licence](https://img.shields.io/github/license/cosmic-plus/cloudflare-federation-server.svg)
[![Dependencies](https://badgen.net/david/dep/cosmic-plus/cloudflare-federation-server)](https://david-dm.org/cosmic-plus/cloudflare-federation-server)

A simple Stellar federation server implementation that uses Cloudflare workers.

(Weekly updates: [Reddit](https://reddit.com/r/cosmic_plus),
[Twitter](https://twitter.com/cosmic_plus),
[Keybase](https://keybase.io/team/cosmic_plus),
[Telegram](https://t.me/cosmic_plus))

## Introduction

This is a [federation
server](https://www.stellar.org/developers/guides/anchor/3-federation-server.html)
implementation running in the cloud using [Cloudflare
Workers](https://www.cloudflare.com/products/cloudflare-workers/). It features
federated address lookup using a simple `addressbook.json` file.

The structure of the address book is as follow:

```js
{
  "hello*example.org": {
    "account_id": "GAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAWHF",
    "memo_type": "text",
    "memo": "hello"
  },
  ...
}
```

The advantage of using Cloudflare is that it offers the lightest - hence
cheapest - cloud workers implementation. At that time (2019-12), the first 100k
daily requests are free of charge. This is more than enough for most use cases.

## Demonstration

This federation server is used by [Cosmic.plus](https://cosmic.plus) and
[Cosmic.link](https://cosmic.link) since mid-2019. It's being used to resolve
addresses such as `tips*cosmic.plus` and `gils*cosmic.plus`.

You can play with Cosmic.plus' instance of the worker here: [worker
preview](https://cloudflareworkers.com/?hide_editor#://federation.cosmic.plus/?type=name&q=tips*cosmic.plus).

## Usage

### Setup the Federation server

_If you're not familiar with Cloudflare Workers, please check the [Cloudflare
Workers Quick Start
Guide](https://developers.cloudflare.com/workers/quickstart/) first._

**Step 1: Clone the Template**

```
wrangler generate federation-server https://git.cosmic.plus/cloudflare-federation-server
```

**Step 2: Edit addressbook.json**

```
cd federation-server
nano addressbook.json
```

**Step 3: Setup wrangler.toml**

```
wrangler config
```

**Step 4: Publish**

```
wrangler publish
```

### Link the Federation Server to a Domain

Edit or create the file at `https://${domain}/.well-known/stellar.toml` and
add the following entry:

```toml
FEDERATION_SERVER = "${federation_server_url}"
```

_Note: it is possible to use the same federation server for several domains._

## Links

**Organization:** [Cosmic.plus](https://cosmic.plus/) | [@GitHub](https://git.cosmic.plus) | [@NPM](https://www.npmjs.com/search?q=cosmic-plus)

**Follow:** [Reddit](https://reddit.com/r/cosmic_plus) | [Twitter](https://twitter.com/cosmic_plus) | [Medium](https://medium.com/cosmic-plus) | [Codepen](https://codepen.io/cosmic-plus)

**Talk:** [Telegram](https://t.me/cosmic_plus) | [Keybase](https://keybase.io/team/cosmic_plus)
