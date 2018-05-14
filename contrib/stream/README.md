# Streaming Trigger

This module builds a MarketStore trigger which pushes data through MarketStore's
streaming interface. The push is triggered by writes to the on-disk data, both
in the base timeframe as well as the aggregates. Aggregated data entries will be 
placed on a 'shelf' and will be given a shelf-life that indicates when they will 
be delivered. These entries will be updated with the latest aggregated candle up 
until the expiration time.

## Configuration
stream.so comes with the server by default, so you can simply configure it
in MarketStore configuration file.  Add the following to your config file.

```
triggers:
    - module: stream.so
      on: */*/*
      config:
          filter: "nasdaq"
```

If filter is set to `nasdaq`, it filters pushes 1D and above timeframes based on 
NASDAQ market hours.

## Build
If you need to change the code, you can build it from this directory by:

```
$ make all
```

It installs the new .so file to the first GOPATH/bin directory.


## Caveat
Since this is implemented based on the Go's plugin mechanism, it is supported only
on Linux as of Go 1.9
