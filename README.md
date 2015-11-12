# falkhash
```
Exotic Probably Shitty Hash

WARNING: This is NOT meant to be a crypto hash. Do not use this for crypto!!!

WARNING 2: I do not do crypto. I made this up by randomly testing things until
it passed all of smhashers tests. It is likely that this hash is heavily
flawed and smhasher just doesn't stress its flaws.

So this was a fun hash that I came up with when I was looking for a 128-bit
hash for falkervisor's code coverage database. This hash passes all of
smhasher's tests, faster than any other hash that does the same. This was
specifically designed for AMD64 processors, but it also performs very well on
Intel processors. This hashing algorithm is not meant to be general purpose,
and without the aesenc instruction it would perform poorly on other/older
architectures.

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
Changelog

falkhash v2 (hash values will change!!!):

Removed assembly implementation in favor for a clang/icc/msvc/gcc
cross-compatible C implementation using intrinsics. Depending on the compiler
performance is increased over the assembly version.

As per funny-falcon's suggestions, each block is xored with the seed, and all
places where aesenc was done with itself, it now uses the seed.

falkhash v1 (hash values will change!!!):

Initial commit

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Performance stats for AMD and Intel:

GCC 4.9.2
AMD Opteron 6376
Cycles per byte 0.174003

clang 3.5.0
AMD Opteron 6376 (clang is pretty slow for this hash sadly, havent tried 3.7.0)
Cycles per byte 0.250947

MSVC 19.00.23026
Intel Xeon E5645
Cycles per byte 0.159220

MSVC 19.00.23026
Intel Core i7 970
Cycles per byte 0.198709

SMHasher output:

--- Testing falkhash (falkhash)

[[[ Sanity Tests ]]]

Verification value 0x7FA15220 : Passed!
Running sanity check 1..........PASS
Running sanity check 2..........PASS

[[[ Speed Tests ]]]

Bulk speed test - 262144-byte keys
Alignment  0 -  5.910 bytes/cycle - 16907.35 MiB/sec @ 3 ghz
Alignment  1 -  5.010 bytes/cycle - 14332.50 MiB/sec @ 3 ghz
Alignment  2 -  4.994 bytes/cycle - 14287.78 MiB/sec @ 3 ghz
Alignment  3 -  4.994 bytes/cycle - 14286.69 MiB/sec @ 3 ghz
Alignment  4 -  4.993 bytes/cycle - 14284.95 MiB/sec @ 3 ghz
Alignment  5 -  4.994 bytes/cycle - 14287.97 MiB/sec @ 3 ghz
Alignment  6 -  4.994 bytes/cycle - 14288.97 MiB/sec @ 3 ghz
Alignment  7 -  4.994 bytes/cycle - 14288.66 MiB/sec @ 3 ghz

Small key speed test -    1-byte keys -   136.00 cycles/hash
Small key speed test -    2-byte keys -   135.21 cycles/hash
Small key speed test -    3-byte keys -   133.99 cycles/hash
Small key speed test -    4-byte keys -   136.00 cycles/hash
Small key speed test -    5-byte keys -   136.00 cycles/hash
Small key speed test -    6-byte keys -   136.00 cycles/hash
Small key speed test -    7-byte keys -   136.87 cycles/hash
Small key speed test -    8-byte keys -   135.00 cycles/hash
Small key speed test -    9-byte keys -   135.00 cycles/hash
Small key speed test -   10-byte keys -   134.31 cycles/hash
Small key speed test -   11-byte keys -   134.00 cycles/hash
Small key speed test -   12-byte keys -   135.00 cycles/hash
Small key speed test -   13-byte keys -   134.00 cycles/hash
Small key speed test -   14-byte keys -   134.88 cycles/hash
Small key speed test -   15-byte keys -   134.16 cycles/hash
Small key speed test -   16-byte keys -   134.00 cycles/hash
Small key speed test -   17-byte keys -   141.32 cycles/hash
Small key speed test -   18-byte keys -   141.98 cycles/hash
Small key speed test -   19-byte keys -   141.00 cycles/hash
Small key speed test -   20-byte keys -   141.91 cycles/hash
Small key speed test -   21-byte keys -   141.00 cycles/hash
Small key speed test -   22-byte keys -   141.99 cycles/hash
Small key speed test -   23-byte keys -   141.54 cycles/hash
Small key speed test -   24-byte keys -   141.00 cycles/hash
Small key speed test -   25-byte keys -   137.00 cycles/hash
Small key speed test -   26-byte keys -   140.99 cycles/hash
Small key speed test -   27-byte keys -   142.03 cycles/hash
Small key speed test -   28-byte keys -   142.92 cycles/hash
Small key speed test -   29-byte keys -   141.00 cycles/hash
Small key speed test -   30-byte keys -   142.07 cycles/hash
Small key speed test -   31-byte keys -   142.44 cycles/hash

[[[ Differential Tests ]]]

Testing 8303632 up-to-5-bit differentials in 64-bit keys -> 128 bit hashes.
1000 reps, 8303632000 total tests, expecting 0.00 random collisions..........
0 total collisions, of which 0 single collisions were ignored

Testing 11017632 up-to-4-bit differentials in 128-bit keys -> 128 bit hashes.
1000 reps, 11017632000 total tests, expecting 0.00 random collisions..........
0 total collisions, of which 0 single collisions were ignored

Testing 2796416 up-to-3-bit differentials in 256-bit keys -> 128 bit hashes.
1000 reps, 2796416000 total tests, expecting 0.00 random collisions..........
0 total collisions, of which 0 single collisions were ignored


[[[ Avalanche Tests ]]]

Testing  32-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.794000%
Testing  40-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.664000%
Testing  48-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.652667%
Testing  56-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.708667%
Testing  64-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.712667%
Testing  72-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.771333%
Testing  80-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.778000%
Testing  88-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.899333%
Testing  96-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.933333%
Testing 104-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.762000%
Testing 112-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.691333%
Testing 120-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.754000%
Testing 128-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.734000%
Testing 136-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.716000%
Testing 144-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.780000%
Testing 152-bit keys -> 128-bit hashes,   300000 reps.......... worst bias is 0.738000%

[[[ Keyset 'Cyclic' Tests ]]]

Keyset 'Cyclic' - 8 cycles of 16 bytes - 10000000 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 100 - 0.038%

Keyset 'Cyclic' - 8 cycles of 17 bytes - 10000000 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 101 - 0.038%

Keyset 'Cyclic' - 8 cycles of 18 bytes - 10000000 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  54 - 0.029%

Keyset 'Cyclic' - 8 cycles of 19 bytes - 10000000 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  72 - 0.048%

Keyset 'Cyclic' - 8 cycles of 20 bytes - 10000000 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  93 - 0.039%


[[[ Keyset 'TwoBytes' Tests ]]]

Keyset 'TwoBytes' - up-to-4-byte keys, 652545 total keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  15-bit window at bit  79 - 0.131%

Keyset 'TwoBytes' - up-to-8-byte keys, 5471025 total keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 126 - 0.062%

Keyset 'TwoBytes' - up-to-12-byte keys, 18616785 total keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  80 - 0.020%

Keyset 'TwoBytes' - up-to-16-byte keys, 44251425 total keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 102 - 0.009%

Keyset 'TwoBytes' - up-to-20-byte keys, 86536545 total keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 111 - 0.004%


[[[ Keyset 'Sparse' Tests ]]]

Keyset 'Sparse' - 32-bit keys with up to 6 bits set - 1149017 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  17-bit window at bit  72 - 0.156%

Keyset 'Sparse' - 40-bit keys with up to 6 bits set - 4598479 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  19-bit window at bit 125 - 0.051%

Keyset 'Sparse' - 48-bit keys with up to 5 bits set - 1925357 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  18-bit window at bit   4 - 0.089%

Keyset 'Sparse' - 56-bit keys with up to 5 bits set - 4216423 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  19-bit window at bit  96 - 0.084%

Keyset 'Sparse' - 64-bit keys with up to 5 bits set - 8303633 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  95 - 0.055%

Keyset 'Sparse' - 96-bit keys with up to 4 bits set - 3469497 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  19-bit window at bit  68 - 0.068%

Keyset 'Sparse' - 256-bit keys with up to 3 bits set - 2796417 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  19-bit window at bit  20 - 0.092%

Keyset 'Sparse' - 2048-bit keys with up to 2 bits set - 2098177 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  18-bit window at bit  39 - 0.108%


[[[ Keyset 'Combination Lowbits' Tests ]]]

Keyset 'Combination' - up to 8 blocks from a set of 8 - 19173960 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 105 - 0.024%


[[[ Keyset 'Combination Highbits' Tests ]]]

Keyset 'Combination' - up to 8 blocks from a set of 8 - 19173960 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  76 - 0.019%


[[[ Keyset 'Combination 0x8000000' Tests ]]]

Keyset 'Combination' - up to 20 blocks from a set of 2 - 2097150 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  18-bit window at bit 114 - 0.115%


[[[ Keyset 'Combination 0x0000001' Tests ]]]

Keyset 'Combination' - up to 20 blocks from a set of 2 - 2097150 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  18-bit window at bit  99 - 0.089%


[[[ Keyset 'Combination Hi-Lo' Tests ]]]

Keyset 'Combination' - up to 6 blocks from a set of 15 - 12204240 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 119 - 0.036%


[[[ Keyset 'Window' Tests ]]]

Keyset 'Windowed' - 256-bit key,  20-bit window - 256 tests, 1048576 keys per test
Window at   0 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   1 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   2 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   3 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   4 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   5 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   6 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   7 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   8 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at   9 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  10 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  11 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  12 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  13 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  14 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  15 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  16 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  17 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  18 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  19 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  20 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  21 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  22 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  23 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  24 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  25 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  26 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  27 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  28 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  29 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  30 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  31 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  32 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  33 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  34 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  35 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  36 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  37 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  38 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  39 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  40 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  41 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  42 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  43 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  44 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  45 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  46 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  47 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  48 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  49 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  50 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  51 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  52 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  53 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  54 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  55 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  56 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  57 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  58 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  59 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  60 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  61 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  62 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  63 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  64 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  65 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  66 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  67 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  68 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  69 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  70 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  71 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  72 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  73 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  74 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  75 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  76 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  77 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  78 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  79 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  80 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  81 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  82 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  83 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  84 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  85 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  86 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  87 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  88 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  89 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  90 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  91 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  92 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  93 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  94 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  95 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  96 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  97 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  98 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at  99 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 100 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 101 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 102 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 103 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 104 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 105 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 106 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 107 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 108 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 109 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 110 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 111 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 112 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 113 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 114 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 115 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 116 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 117 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 118 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 119 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 120 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 121 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 122 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 123 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 124 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 125 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 126 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 127 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 128 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 129 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 130 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 131 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 132 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 133 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 134 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 135 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 136 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 137 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 138 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 139 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 140 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 141 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 142 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 143 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 144 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 145 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 146 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 147 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 148 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 149 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 150 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 151 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 152 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 153 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 154 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 155 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 156 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 157 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 158 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 159 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 160 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 161 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 162 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 163 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 164 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 165 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 166 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 167 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 168 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 169 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 170 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 171 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 172 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 173 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 174 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 175 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 176 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 177 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 178 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 179 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 180 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 181 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 182 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 183 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 184 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 185 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 186 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 187 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 188 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 189 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 190 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 191 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 192 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 193 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 194 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 195 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 196 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 197 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 198 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 199 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 200 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 201 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 202 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 203 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 204 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 205 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 206 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 207 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 208 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 209 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 210 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 211 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 212 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 213 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 214 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 215 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 216 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 217 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 218 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 219 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 220 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 221 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 222 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 223 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 224 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 225 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 226 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 227 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 228 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 229 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 230 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 231 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 232 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 233 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 234 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 235 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 236 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 237 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 238 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 239 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 240 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 241 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 242 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 243 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 244 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 245 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 246 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 247 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 248 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 249 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 250 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 251 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 252 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 253 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 254 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 255 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Window at 256 - Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)

[[[ Keyset 'Text' Tests ]]]

Keyset 'Text' - keys of form "Foo[XXXX]Bar" - 14776336 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit 125 - 0.019%

Keyset 'Text' - keys of form "FooBar[XXXX]" - 14776336 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  63 - 0.026%

Keyset 'Text' - keys of form "[XXXX]FooBar" - 14776336 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  20-bit window at bit  55 - 0.028%


[[[ Keyset 'Zeroes' Tests ]]]

Keyset 'Zeroes' - 65536 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  12-bit window at bit 126 - 0.373%


[[[ Keyset 'Seed' Tests ]]]

Keyset 'Seed' - 1000000 keys
Testing collisions   - Expected     0.00, actual     0.00 ( 0.00x)
Testing distribution - Worst bias is the  17-bit window at bit  17 - 0.119%



Input vcode 0x00000001, Output vcode 0x00000001, Result vcode 0x00000001
Verification value is 0x00000001 - Testing took -124.444326 seconds
```

