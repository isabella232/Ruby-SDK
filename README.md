# WePay SDK for Ruby

[![Source](http://img.shields.io/badge/source-wepay/Ruby–SDK-blue.svg?style=flat-square)](https://github.com/wepay/Ruby-SDK)
[![Latest Stable Version](https://img.shields.io/gem/v/wepay.svg?style=flat-square)](https://rubygems.org/gems/wepay)
[![Total Downloads](https://img.shields.io/gem/dt/wepay.svg?style=flat-square)](https://rubygems.org/gems/wepay)
[![Open Issues](http://img.shields.io/github/issues/wepay/Ruby-SDK.svg?style=flat-square)](https://github.com/wepay/Ruby-SDK/issues)
[![Build Status](http://img.shields.io/travis/wepay/Ruby-SDK/master.svg?style=flat-square)](https://travis-ci.org/wepay/Ruby-SDK)
[![Coverage Status](http://img.shields.io/coveralls/wepay/Ruby-SDK/master.svg?style=flat-square)](https://coveralls.io/r/wepay/Ruby-SDK?branch=master)
[![Code Climate](http://img.shields.io/codeclimate/github/wepay/Ruby-SDK.svg?style=flat-square)](https://codeclimate.com/github/wepay/Ruby-SDK)
[![Code Quality](http://img.shields.io/scrutinizer/g/wepay/Ruby-SDK.svg?style=flat-square)](https://scrutinizer-ci.com/g/wepay/Ruby-SDK)
[![Author](http://img.shields.io/badge/author-@wepay-blue.svg?style=flat-square)](https://github.com/wepay)
[![Author](http://img.shields.io/badge/author-@skyzyx-blue.svg?style=flat-square)](https://github.com/skyzyx)

Check out our developer docs at https://stage.wepay.com/developer for more
information, or you may email <api@wepay.com> if you have any other questions.

This project uses [Semantic Versioning](http://semver.org) for managing
backwards-compatibility.

> **NOTE:** Version 0.4.0 is not strictly backwards-compatible with the earlier 0.0.x versions.

> **NOTE:** Due to impending PCI 3.x changes, we will be disabling support for TLS < 1.2 over our API. TLS 1.2 support requires Ruby 2.0.0. As such, while this SDK may function with Ruby 1.9, we no longer support it.

* [API Reference](https://wepay.github.io/Ruby-SDK/)

## Installation

```ruby
gem 'wepay', '~> 0.4.0'
```

And include it in your scripts:

```ruby
require 'wepay'
```

## Examples

```ruby
client_id = 'your_client_id'
client_secret = 'your_client_secret'
use_stage = true

wepay = WePay::Client.new(client_id, client_secret, use_stage)

# Get the OAuth 2.0 authorization URL. Send the user to this URL to authorize
# the application, then they will return to your `redirect_uri` with a code as
# a GET parameter.
redirect_uri = "http://myexamplesite.com/wepay"
redirect_to(wepay.oauth2_authorize_url(redirect_uri))

# Once you have the OAuth 2.0 code, you can request an access token.
response = wepay.oauth2_token(code, redirect_uri)
access_token = response['access_token']

# Make a call to the `/user` endpoint (which requires no parameters).
response = wepay.call('/user', access_token)

# You may also open a payment account for the user.
response = wepay.call('/account/create', access_token, {
  :name        => "test account",
  :description => "this is only a test"
})
```

## Testing

Firstly, run `bundle install` to download and install the dependencies.

You can run the tests as follows:

```bash
make test
```


## API Reference

The API Reference is generated by a tool called [YARD](http://yardoc.org). Once it's installed, you can generate
updated documentation by running the following command in the root of the repository.

```bash
make docs
```

## Contributing
Here's the process for contributing:

1. Fork Signer to your GitHub account.
2. Clone your GitHub copy of the repository into your local workspace.
3. Write code, fix bugs, and add tests with 100% code coverage.
4. Commit your changes to your local workspace and push them up to your GitHub copy.
5. You submit a GitHub pull request with a description of what the change is.
6. The contribution is reviewed. Maybe there will be some banter back-and-forth in the comments.
7. If all goes well, your pull request will be accepted and your changes are merged in.


## Authors, Copyright & Licensing

* Copyright (c) 2012–2017 [WePay](http://wepay.com)

See also the list of [contributors](https://github.com/wepay/Ruby-SDK/graphs/contributors) who participated in this project.

Licensed for use under the terms of the [Apache 2.0] license.

  [Apache 2.0]: http://opensource.org/licenses/Apache-2.0
