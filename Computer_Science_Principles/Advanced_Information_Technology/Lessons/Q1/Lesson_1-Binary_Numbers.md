
## Binary Numbers

As humans, we typically represent numbers in the **decimal** system. Counting to ten is as simple as __1, 2, 3, 4, 5, 6, 7, 8, 9, 10__.

As we just learned, computers represent all information in __bits__. In order to represent numbers with just __0__ s and __1__ s, computers use the __binary__ number system. Here's what it looks like when a computer counts to ten: `0001`, `0010`, `0011`, `0100`, `0101`, `0110`, `0111`, `1000`, `1001`, `1010`.

### Refresher: Decimal System

Before exploring how the binary system works, let's revisit our old friend, the decimal system. When you learned how to count, you might have learned that the right-most digit is the "ones' place", the next is the "tens' place", the next is the "hundreds' place", etc.
Another way to say that is that the digit in the right-most position is multiplied by __1__ , the digit one place to its left is multiplied by __10__ , and the digit two places to its left is multiplied by __100__.
Let's visualize the number __234__:

|    2     |  3   |  4   |
| :------: | :--: | :--: |
| Hundreds | Tens | Ones |
|   100    |  10  |  1   |
When we multiply each digit by its place, we can see that __234__ is equal to:

|    2     |    3    |   4    |
| :------: | :-----: | :----: |
| Hundreds |  Tens   |  Ones  |
|   100    |   10    |   1    |
| (2\*100) | (3\*10) | (4\*1) |
(2\*100) + (3\*10) + (4\*1)
200 + 30 + 4
234

We can also think of those places in terms of the powers of ten. The ones' place represents multiplying by ‍10$^0$, the tens' place represents multiplying by ‍10$^1$, and the hundreds' place represents multiplying by 10$^2$. Each place we add, we're multiplying the digit in that place by the next power of __10__.

|    2     |   3    |    4    |
| :------: | :----: | :-----: |
| Hundreds |  Tens  |  Ones   |
|   100    |   10   |    1    |
|  10$^2$  | 10$^1$ | ‍10$^0$ |
### Binary System

#### Binary to Decimal

The binary system works the same way as decimal. The only difference is that instead of multiplying the digit by a power of __10__, we multiply it by a power of __2__.

Let's look at the decimal number __1__, represented in binary as: __0001__.

|   0    |   0    |   0    |   1    |
| :----: | :----: | :----: | :----: |
| Eights | Fours  |  Twos  |  Ones  |
|   8    |   4    |   2    |   1    |
| 2$^3$  | 2$^2$  | 2$^1$  | 2$^0$  |
| (0\*8) | (0\*4) | (0\*2) | (1\*1) |
(0\*8) + (0\*4) + (0\*2) + (1\*1)
0 + 0 + 0 + 1
1

Okay, perhaps you could have guessed that one — now for a bigger number!
The decimal number __10__ is represented in binary as __1010__:

|   1    |   0    |   1    |   0    |
| :----: | :----: | :----: | :----: |
| Eights | Fours  |  Twos  |  Ones  |
|   8    |   4    |   2    |   1    |
| 2$^3$  | 2$^2$  | 2$^1$  | 2$^0$  |
| (1\*8) | (0\*4) | (1\*2) | (0\*1) |
(1\*8) + (0\*4) + (1\*2) + (0\*1)
8 + 0 + 2 + 0
10

#### Decimal to Binary

To convert a decimal number into binary we first need to consider how many digits we will need. Let's take the number __132__. We'll definitely need more than four bits, because the largest number we can make with just four bits is 15 (8 + 4 + 2 + 1).

>[!TIP]
> We don't have to add up every place value to determine the largest number that they would fit. Instead, we can ask how large the next place value would be and subtract one. When going from four bits to five bits, the next place value would be the sixteens' place. Subtract one and we get 15.

So how many bits do we need to hold __132__? Let's count up.

| __Bits__ | __Place Value__ | __Max Value__ |
| :------: | :-------------: | :-----------: |
|    1     |        1        |       1       |
|    2     |        2        |       3       |
|    3     |        4        |       7       |
|    4     |        8        |      15       |
|    5     |       16        |      31       |
|    6     |       32        |      63       |
|    7     |       64        |      127      |
|    8     |       128       |      255      |

Looks like eight bits will do. The next step is to find out which bits will need to be __ones__ and which will need to be __zeros__. To do this, we need to go from left-to-right, and if the number of the current place value we are looking at is less than or equal to our current number, then it is a __one__ otherwise it is a __zero__.

|  1  |     |     |     |     |     |     |     |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 | 64  | 32  | 16  |  8  |  4  |  2  |  1  |

__128__ is less than or equal to __132__, so we'll put a __1__ for that bit. We now need to subtract __128__ from our number, because that bit represents the number __128__. __132__ minus __128__ is __4__, and now that becomes our current number.

|  1  |  0  |     |     |     |     |     |     |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 | 64  | 32  | 16  |  8  |  4  |  2  |  1  |

__64__ is larger than our current number, so we put a __zero__ in that bit and move on. We'll keep placing zeros until we get to a number that is less than or equal to __4__.

|  1  |  0  |  0  |  0  |  0  |     |     |     |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 | 64  | 32  | 16  |  8  |  4  |  2  |  1  |

__32__, __16__, and __8__ are all greater than __4__, so they are also __zeros__.

|  1  |  0  |  0  |  0  |  0  |  1  |     |     |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 | 64  | 32  | 16  |  8  |  4  |  2  |  1  |

__4__ is less than or equal to __4__, so that bit is a __one__. __4__ minus __4__ is __0__, so that is now our current number. When we get to __0__ we are done, so all the other bits will be __zeros__.

|  1  |  0  |  0  |  0  |  0  |  1  |  0  |  0  |
| :-: | :-: | :-: | :-: | :-: | :-: | :-: | :-: |
| 128 | 64  | 32  | 16  |  8  |  4  |  2  |  1  |

And there we have it __10000100__ is binary for 132.