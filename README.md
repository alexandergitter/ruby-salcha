# ChaCha20

A pure Ruby implementation of the Salsa20 and ChaCha20 stream ciphers. Supports arbitrary seeking inside the keystream.

## Installation

For the time being, this is not on rubygems.org. Point your Gemfile to this repository.

## Usage

Initialize a new cipher with a 32-byte key and an 8-byte nonce (both bytestrings of class `String`):

```ruby
cipher = ChaCha20::Cipher.new(key, nonce)
```

You can then encrypt or decrypt data with the `encrypt` and `decrypt` methods:

```ruby
ciphertext = cipher.encrypt(plaintext)
plaintext = cipher.decrypt(ciphertext)
```

Note that these methods advance the internal position inside the key stream, so you can keep calling them for chunk-wise
de-/encryption. If you want to jump to a specific byte-position in the key stream, you can use the `seek` method:

```ruby
cipher.seek(4711)
```
