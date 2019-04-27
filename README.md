# Haskell project ideas

This is a list of ideas for Haskell open-source projects. Most of these ideas are centered around problems that I've run into in the real world.

This list is in the public domain; you may implement any of these projects, and you do not have to give me credit. If you, the reader, have project ideas, open a PR and I'll add them.

# Effect implementations
* Structured logging with [katip](http://hackage.haskell.org/package/katip). (★★)
* `Memo`, a là `Control.Monad.Memo`. (★★★)
* Region-based resource management as [described by Oleg](http://okmij.org/ftp/Haskell/regions.html). (★★★★★)
* RWSC carrier interpreting (Reader r :+: Writer w :+: State s) (★)
* Delimited continuations (this may or may not be possible) (💀)

# Algorithms
* Implement a function from `Double -> String` based on ["Ryū: Fast Float-to-String Conversion"](https://dl.acm.org/citation.cfm?id=3192369). (★★★)

# Data structures
* Time-based UUID library. Cassandra and many other networked servers provide a `uuidtime` data type, which stores a UUID that has its date encoded in its first few bytes, such that the output of successive generated `uuidtime` is roughly in sorted order, and that there exists a function to reconstruct at least the day part of the `uuidtime`. (★★)
* Validation library for JSON structures. The `aeson` package is great and performant but complects validation and decoding of JSON data. Build a library that uses recursion schemes to check validity of a JSON `Value` and reports all possible errors at once, a la the `Validation` monad. (★★)
* Natural-language date/time parser. You could fork [duckling](https://duckling.wit.ai). (★★★★)
* While you're at it, you could create a new date/time library, which would be most welcome for those of us who have suffered the differences between `Day`, `Date`, `LocalTime` and `UTCTime`. The difficulty here is in ensuring compatibility with the whole ecosystem of libraries that use `UTCTime`.

# Web programming
* Declarative interface to [airship](http://hackage.haskell.org/package/airship) using some sort of deep embedding. (★)
* Library for HTTP tracing with [lightstep](https://lightstep.com). [`haskell-opentracing`](https://github.com/ocharles/haskell-opentracing) might be somewhere to start. (★★★)
* Bridge between `network` and `System.Event`, a la Netty. (★★★★)

# macOS
* Bridge to [`NSLinguisticTagger`](https://developer.apple.com/documentation/foundation/nslinguistictagger) and [`NSOrthography`](https://developer.apple.com/documentation/foundation/nsorthography) for natural language processing. (★)

# Unix
* Declarative library for command line interfaces, a là [cobra](https://github.com/spf13/cobra). (★★★)
* Library for integration with [systemd socket activation](http://0pointer.de/blog/projects/socket-activation.html). (★★★)
* Library to pull configuration records from environment variables. Given the environment variables `MYAPP_PORT=33`, `MYAPP_URL=foo`, and `MYAPP_NAME=go`, and a corresponding record type

``` haskell
data Env = Env { port :: Int, url :: String, name :: String}
  deriving (Generic, FromJSON)

fromEnv :: FromJSON e => IO (Either String e)
```

I should be able to run `fromEnv "myApp"` and get back an `Env` with values filled in from the environment variables. (★ for piggybacking off of `aeson`, ★★★ for a fresh `Generic` implementation).
