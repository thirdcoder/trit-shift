# trit-shift

Trit shifting operations

Usage:

    var shl = require('trit-shift').shl;
    var shr = require('trit-shift').shr;

    // shift left
    shl(input, carryIn);
    shl(1, 0);  // 1 ('01') -> 3 ('10'), shift in zero from left
    shl(1, -1); // 1 ('01') -> 2 ('1i'), shift in negative from left

    // shift right
    shr(input, width, carryIn);
    shr(3, 5, 0); // 3 ('10') -> 1 ('01'), shifted right

Balanced ternary base 3 trit shifting, analogous to
base 2 [bit shifting](https://en.wikipedia.org/wiki/Bitwise_operation#Bit_shifts) operations.
See also [balanced-ternary](https://github.com/thirdcoder/balanced-ternary).

Both shift left and shift right take a required parameter for the trit to shift in (`carryIn`);
zero is not assumed since shifting in -1 or +1 may be desired (for example, for tritmasks).
Shifting left is equivalent to multiplication by three, plus the carry:

    shl(x, 0);  // x * 3
    shl(x, 1);  // x * 3 + 1
    shl(x, -1); // x * 3 - 1

Shifting right is equivalent to division by three, rounded to the nearest integer, plus the
carry input trit at the most-significant trit position (which is why the `width` parameter
is required, set to number of trits in the input value).

    shr(x, N, 0);   // Math.round(x / 3)

Used to simulate ternary shift registers. The shifted-out value is not returned but can
be computed separately using [lst](https://github.com/thirdcoder/lst) for `shr`, and
[trit-getset](https://github.com/thirdcoder/trit-getset) at the most significant trit for
`shl`.
