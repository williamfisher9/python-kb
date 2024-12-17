# DECIMAL MODULE
Python decimal module that supports fast correctly-rounded decimal floating-point arithmetic.

Many decimal numbers don’t have exact representations in binary floating-point such as 0.1. When using these numbers in arithmetic operations, you’ll get a result that you would not expect.
```
x = 0.1
y = 0.1
z = 0.1
print(x)
print(y)
print(z)
print(x + y + z)    # 0.30000000000000004
```

To solve this problem, use the Decimal class from the decimal module as follows:
```
import decimal
from decimal import Decimal

x = Decimal('0.1')
y = Decimal('0.1')
z = Decimal('0.1')

print(x + y + z)    # 0.3
```

Unlike floats, Python represents decimal numbers exactly. And the exactness carries over into arithmetic.

### Decimal context
Decimal always associates with a context that controls the following aspects:
- Precision during an arithmetic operation
- Rounding algorithm

By default, the context is global. The global context is the default context. To get the default context, you call the getcontext() function from the decimal module: `decimal.getcontext()`

The getcontext() function returns the default context, which can be global or local. To create a new context copied from another context, you use the localcontext() function: `decimal.localcontext(ctx=None)`. 
The localcontext() returns a new context copied from the context ctx if specified.
```
import decimal
from decimal import Decimal


ctx = decimal.getcontext()
ctx.rounding = decimal.ROUND_HALF_UP

x = Decimal('2.25')
y = Decimal('3.35')

print(round(x, 1))    # 2.3
print(round(y, 1))    # 3.4
```

Default rounding mechanism is 'ROUND_HALF_EVEN'.

```
# the local context doesn’t affect the global context. After the with block, Python uses the default rounding mechanism.
import decimal
from decimal import Decimal


x = Decimal('2.25')
y = Decimal('3.35')

with decimal.localcontext() as ctx:
    print('Local context:')
    ctx.rounding = decimal.ROUND_HALF_UP
    print(round(x, 1))                        # 2.3
    print(round(y, 1))                        # 3.4

print('Global context:')                      # default rounding 'ROUND_HALF_EVEN'
print(round(x, 1))                            # 2.2
print(round(y, 1))                            # 3.4
```

### Decimal Constructor
```
Decimal(value='0', context=None)
```
The value argument can be an integer, string, tuple, float, or another Decimal object. If you don’t provide the value argument, it defaults to '0'.

If the value is a tuple, it should take `(sign, (digit1,digit2, digit3,...), exponent)` where sign is 0 for positive and 1 for negative. An example is 3.14 where the input  will be:
```
import decimal
from decimal import Decimal

x = Decimal((0, (3, 1, 4), -2))
print(x)
```

Notice that the decimal context precision only affects the arithmetic operation, not the Decimal constructor. 

When you use a float that doesn’t have an exact binary float representation, the Decimal constructor cannot create an accurate decimal representation. 
So in practice we will only use a string or a tuple to represent a number. For example:
```
import decimal
from decimal import Decimal

x = Decimal(0.1)
print(x)                # 0.1000000000000000055511151231257827021181583404541015625
```

When you use functions from the math module for decimal numbers, Python will cast the Decimal objects to floats before carrying arithmetic operations. 
This results in losing the precision built in the decimal objects.

The Decimal class doesn't have all methods defined in the math module. However, you should use the Decimal's arithmetic methods if they’re available.
