Bloomex [![Build Status](https://img.shields.io/travis/gmcabrita/bloomex.svg?style=flat)](https://travis-ci.org/gmcabrita/bloomex) [![Coverage Status](https://img.shields.io/coveralls/gmcabrita/bloomex.svg?style=flat)](https://coveralls.io/r/gmcabrita/bloomex?branch=master) [![Hex docs](http://img.shields.io/badge/hex.pm-docs-green.svg?style=flat)](https://hexdocs.pm/bloomex) [![Hex Version](http://img.shields.io/hexpm/v/bloomex.svg?style=flat)](https://hex.pm/packages/bloomex) [![License](http://img.shields.io/hexpm/l/bloomex.svg?style=flat)](https://github.com/gmcabrita/bloomex/blob/master/LICENSE)
=======

Bloomex is a pure Elixir implementation of [Scalable Bloom Filters](http://haslab.uminho.pt/cbm/files/dbloom.pdf).

# Usage

Add Bloomex as a dependency in your mix.exs file.

```elixir
def deps do
  [{:bloomex, "~> 0.2"}]
end
```

When you are done, run `mix deps.get` in your shell to fetch and compile Bloomex.

# Examples

```iex
iex> bf = Bloomex.scalable(1000, 0.1, 0.1, 2)
%Bloomex.ScalableBloom...
iex> bf = Bloomex.add(bf, 5)
%Bloomex.ScalableBloom...
iex> Bloomex.member?(bf, 5)
true
iex> bf = Bloomex.add(bf, 100)
%Bloomex.ScalableBloom...
iex> Bloomex.member?(bf, 100)
true
iex> Bloomex.member?(bf, 105)
false
iex> Bloomex.member?(bf, 101) # false positive
true
```

You can also pass in a hashing function to be used by the Bloom filter when creating one.

(assuming we have [Murmur](https://hex.pm/packages/murmur/) installed as a dependency)

```iex
iex> bf = Bloomex.scalable(1000, 0.1, 0.1, 2, &(Murmur.hash(:x86_128, &1)))
%Bloomex.ScalableBloom...
iex> bf = Bloomex.add(bf, 5)
%Bloomex.ScalableBloom...
iex> Bloomex.member?(bf, 5)
true
iex> bf = Bloomex.add(bf, 100)
%Bloomex.ScalableBloom...
iex> Bloomex.member?(bf, 100)
true
iex> Bloomex.member?(bf, 105) # false positive
true
iex> Bloomex.member?(bf, 101)
false
``````
