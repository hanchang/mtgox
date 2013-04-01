# Ruby wrapper for the Mt. Gox Trade API

[![Gem Version](https://badge.fury.io/rb/mtgox.png)][gem]
[![Build Status](https://secure.travis-ci.org/sferik/mtgox.png?branch=master)][travis]
[![Dependency Status](https://gemnasium.com/sferik/mtgox.png?travis)][gemnasium]
[![Code Climate](https://codeclimate.com/github/sferik/mtgox.png)][codeclimate]
[![Coverage Status](https://coveralls.io/repos/sferik/mtgox/badge.png?branch=master)][coveralls]

[gem]: https://rubygems.org/gems/mtgox
[travis]: http://travis-ci.org/sferik/mtgox
[gemnasium]: https://gemnasium.com/sferik/mtgox
[codeclimate]: https://codeclimate.com/github/sferik/mtgox
[coveralls]: https://coveralls.io/r/sferik/mtgox

Mt. Gox allows you to trade US Dollars (USD) for Bitcoins (BTC) or Bitcoins for
US Dollars.

## Installation
    gem install mtgox

To ensure the code you're installing hasn't been tampered with, it's
recommended that you verify the signature. To do this, you need to add my
public key as a trusted certificate (you only need to do this once):

    gem cert --add <(curl -Ls https://gist.github.com/sferik/4701180/raw/public_cert.pem)

Then, install the gem with the high security trust policy:

    gem install mtgox -P HighSecurity

## Executable
After installing the gem, you can get the current price for 1 BTC in USD by
typing `btc` in your bash shell:

    $ btc
    50.00


## Documentation
[http://rdoc.info/gems/mtgox][documentation]

[documentation]: http://rdoc.info/gems/mtgox

## Usage Examples
    require 'rubygems'
    require 'mtgox'

    puts MtGox.ticker
    <MtGox::Ticker:0x000000029b8258
     @buy=93.01005,
     @high=93.8,
     @low=91.0,
     @previous_price=nil,
     @price=93.44999,
     @sell=93.44999,
     @volume=20920.0,
     @vwap=92.756087768>

    # Fetch the latest price for 1 BTC in USD
    puts MtGox.ticker.sell

    # Fetch open asks
    puts MtGox.asks
    [#<MtGox::Ask:0x00000002c1f0c8 @price=93.44, @amount=1.30994231>, #<MtGox::Ask:0x00000002c1f050 @price=93.45, @amount=7.47625374>, #<MtGox::Ask:0x00000002c1efd8 @price=93.4588, @amount=8.0>, #<MtGox::Ask:0x00000002c1ef60 @price=93.465, @amount=10.0>, #<MtGox::Ask:0x00000002c1eee8 @price=93.46699, @amount=0.47015735>, #<MtGox::Ask:0x00000002c1ee70 @price=93.467, @amount=11.3277389>, #<MtGox::Ask:0x00000002c1edf8 @price=93.478, @amount=52.12313332>, #<MtGox::Ask:0x00000002c1ed80 @price=93.48799, @amount=5.1760007>, #<MtGox::Ask:0x00000002c1ed08 @price=93.497, @amount=2.99681883>, #<MtGox::Ask:0x00000002c1ec90 @price=93.498, @amount=10.0>, #<MtGox::Ask:0x00000002c1ec18 @price=93.4989, @amount=20.26516861>]

    # Fetch open bids
    puts MtGox.bids

    # Fetch the last 48 hours worth of trades (takes a minute)
    puts MtGox.trades

    # Certain methods require authentication
    MtGox.configure do |config|
      config.key = YOUR_MTGOX_KEY
      config.secret = YOUR_MTGOX_SECRET
    end

    # Fetch your current balance
    puts MtGox.balance
    [#<MtGox::Balance:0x000000014dc2f8 @amount=0.0, @currency="BTC">,
     #<MtGox::Balance:0x000000014dc1e0 @amount=0.0, @currency="USD">]

    # Place a limit order to buy one bitcoin for $0.011
    MtGox.buy! 1.0, 0.011

    # Place a limit order to sell one bitcoin for $100
    MtGox.sell! 1.0, 100.0

    # Cancel order #1234567890
    MtGox.cancel 1234567890

    # Withdraw 1 BTC from your account
    MtGox.withdraw! 1.0, "1KxSo9bGBfPVFEtWNLpnUK1bfLNNT4q31L"

## Contributing
In the spirit of [free software][free-sw], **everyone** is encouraged to help
improve this project.

[free-sw]: http://www.fsf.org/licensing/essays/free-sw.html

Here are some ways *you* can contribute:

* by using alpha, beta, and prerelease versions
* by reporting bugs
* by suggesting new features
* by writing or editing documentation
* by writing specifications
* by writing code (**no patch is too small**: fix typos, add comments, clean up
  inconsistent whitespace)
* by refactoring code
* by closing [issues][]
* by reviewing patches

[issues]: https://github.com/sferik/mtgox/issues

## Supported Ruby Versions
This library aims to support and is [tested against][travis] the following Ruby
implementations:

* Ruby 1.9.2
* Ruby 1.9.3
* Ruby 2.0.0

If something doesn't work on one of these interpreters, it's a bug.

This library may inadvertently work (or seem to work) on other Ruby
implementations, however support will only be provided for the versions listed
above.

If you would like this library to support another Ruby version, you may
volunteer to be a maintainer. Being a maintainer entails making sure all tests
run and pass on that implementation. When something breaks on your
implementation, you will be responsible for providing patches in a timely
fashion. If critical issues for a particular implementation exist at the time
of a major release, support for that Ruby version may be dropped.

## Copyright
Copyright (c) 2011-2013 Erik Michaels-Ober. See [LICENSE][] for details.

[license]: LICENSE.md
