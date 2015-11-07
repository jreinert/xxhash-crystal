# xxhash-crystal

These are the crystal bindings for [xxHash](https://github.com/Cyan4973/xxHash)
- An extremely fast non-cryptographic hash algorithm

## Installation

Add this to your application's `shard.yml`:

```yaml
dependencies:
  xxhash:
    github: jreinert/xxhash-crystal
```

## Usage

This library provides bindings for both the 64 and 32 bit version of xxHash
They are accessed through the modules `XXHash32` and `XXHash64` respectively.

You should use the one that matches your cpu architecture.

```crystal
require "xxhash"

# Pass a nn-bit seed 
seed = (SecureRandom.random_bytes(8).to_unsafe as UInt64*).value
puts XXHash64.hex_digest("foobar", seed)

# Or use 0 by default
puts XXHash64.hex_digest("foobar")

# Stream data
XXHash64.open(seed) do |digester|
  buffer :: UInt8[1024]
  while (len = some_io.read(buffer)) != 0
    digester.write(buffer[0, len])
  end

  puts digester.hex_digest
end
```

## Contributing

1. Fork it ( https://github.com/jreinert/xxhash/fork )
2. Create your feature branch (git checkout -b my-new-feature)
3. Commit your changes (git commit -am 'Add some feature')
4. Push to the branch (git push origin my-new-feature)
5. Create a new Pull Request

## Contributors

- [jreinert](https://github.com/jreinert) Joakim Reinert - creator, maintainer