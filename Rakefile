require "bundler/gem_tasks"
require "minitest/test_task"
require_relative "lib/ruby-salcha"

Minitest::TestTask.create

task default: :test

def read_hex(inp)
  [inp.gsub(/\s+/, "")].pack("H*")
end

task :benchmark do
  require "benchmark"

  key = read_hex("0000000000000000000000000000000000000000000000000000000000000000")
  nonce = read_hex("0000000000000000")
  bytesize = 1024 * 1024 * 10
  puts "Benchmark to generate 10 MB keystream"

  Benchmark.bm do |bm|
    bm.report("Salsa20Specification") { Salcha::Cipher.new(key, nonce, cipher: :salsa20_spec).keystream(bytesize) }
    bm.report("Salsa20Core") { Salcha::Cipher.new(key, nonce, cipher: :salsa20_core).keystream(bytesize) }
    bm.report("ChaCha20") { Salcha::Cipher.new(key, nonce, cipher: :chacha20).keystream(bytesize) }
  end
end
