## Bits and Bytes

### How Do Computers Represent Data?

When we look at a computer, we see text and images and shapes.
To a computer, all of that is just binary data, 1s and 0s.
The following 1s and 0s represents a tiny GIF:

``` txt
010001110100100101000110001110000011100101100001000000010000000000000001000000001000000000000000000000000000000000000000000000001111111111111111111111110010000111111001000001000000000100000000000000000000000000000000001011000000000000000000000000000000000000000001000000000000000100000000000000000000001000000001010001000000000000111011
```

A string of 0 and 1 numbers, 336 numbers long.

This next string of 1s and 0s represents a command to add a number:

``` txt
0001 0001 0000 0101
```

A 16-character long string of 1s and 0s.

You might be scratching your head at this point. Why do computers represent information in such a hard to read way? And how can 1s and 0s represent so many different things? That's what we'll explore in this lesson.

### Binary and Data

Computers use electrical signals, represented as **ones and zeroes**, to store and process all types of information. A single on/off electrical state is called a **bit**, the smallest unit of data. Multiple bits together can represent larger and more complex information using the **binary number system**, where each position represents a power of two.

Binary makes it possible to represent any number, and numbers in turn can represent **letters**, **images**, **sound**, and more:

- **Text:** Each letter is assigned a number, so words become sequences of numeric values stored as bits.
- **Images:** Made of pixels, each with colors represented by numbers. Higher resolution means more data.
- **Audio:** Sound waves can be sampled as numbers; more bits (e.g., 32-bit vs. 8-bit) produce higher-quality sound.

Although modern programmers rarely work directly with binary, **every digital process, input, storage, processing, and output, ultimately relies on these simple on/off electrical signals**. They form the foundation of how computers function internally.

### Bits (Binary Digits)

Computers store information using bits. A bit (short for "binary digit") stores either the value `0` or `1`

#### What fits in a bit?
A single bit can only represent two different values. That's not very much, but that's still enough to represent any two-valued state.

- Is a lightbulb on or off?
- Is a button enabled or disabled?
- Is the current time AM or PM?

#### Sequences of bits

Computers use multiple bits to represent data that is more complex than a simple on/off value.

A sequence of two bits can represent four (2$^2$) distinct values:

- `00`
- `01`
- `10`
- `11`

A sequence of three bits can represent eight (2$^3$) different values:

- `000`
- `001`
- `010`
- `011`
- `100`
- `101`
- `110`
- `111`

A sequence can represent many things: a number, a character, a pixel. Plus, the same sequence can represent different types of data in different contexts. The sequence `01000011` could represent `67` in a calculator application while also representing the letter `C` in a text file.

#### Physical storage
Computers typically store bits using electromechanical transistors which can map electrical signals to either an on or off state.

### Bytes

A bit is the smallest piece of information in a computer, a single value storing either `0` or `1`.

A **byte** is a unit of digital information that consists of `8` of those bits.

Here's a single byte of information: `11110110`

Here are three more bytes of information: `00001010 01010100 11001100`

From bits to bytes
Conversion between bits and bytes is a simple calculation: divide by `8`
to convert from bits to bytes or multiply by `8` to convert from bytes to bits. Try it yourself!

#### Why bytes?

What is so special about `8` bits that it deserves its own name?

Computers do process all data as bits, but they prefer to process bits in byte-sized groupings. Or to put it another way: a byte is how much a computer likes to "bite" at once.

The byte is also the smallest addressable unit of memory in most modern computers. A computer with byte-addressable memory can not store an individual piece of data that is smaller than a byte.

