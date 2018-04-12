Just assign to the destination integer -- `uint32_t lower = static_cast<uint32_t>(my_uint_64)`.

This is safe, from The C++ Programming Language 10.5.2.1

> If the destination type is unsigned, the resulting value is simply as many bits from the source as will fit in the destination (high-order bits are thrown away if necessary);

> If the desination type is signed, the value is unchanged if it can be represented in the destination type; otherwise, the value is **implementation-defined**
