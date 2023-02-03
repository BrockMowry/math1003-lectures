# Lesson 1.6 - Binary Number System
Computers use binary to read and comprehend data. To further understand the process, we need to understand how binary works.

![alt](https://www.unm.edu/~tbeach/terms/images/base2.gif)


## How to convert from binary to a decimal.
Given 1101, convert to it's decimal counterpart:
```
int convert()
{
    string input = "1101";
    char[] inputArray = input.ToCharArray();

    // We need to first reverse the array because binary place values work right to left.
    // We could also adjust the for loop to start at the last index and work that way,
    // but it just easier to work our way up.
    Array.Reverse(inputArray);

    // Store the converted in a variable.
    int sum = 0;

    // Use a for loop to loop through the items in the array.
    for (int i = 0; i < inputArray.Length; i++)
    {
        // Check if the item in the array at i is not zero.
        // If it is, continue to the next item because zeros are ignored in binary calculations.
        if (inputArray[i] == '0')
            continue;

        // If the current iteration (i) is 0, just add 1 because it is in the ones digit (place value). This is why we reverse the number :).
        if (i == 0)
            sum += 1;

        // If not, square the iteration index (i) and add it to the sum.
        else
            sum += Convert.ToInt32(Math.Pow(2, i))
    }

    // Return the converted value.
    // This will be the converted decimal.
    return sum;
}
```

This could be written out like this:
```
Starting with 1101:
- Reverse it to become 1011.

There is a 1 in the ones column, so we start the equation with +1
There is a 0 in the twos column, so we ignore it.
There is a 1 in the fours column, so we add 4 to the equation.
There is a 1 in the eights column, so we add 8 to the equation.

After finishing with each digit, we can finalize our equation:
1 + 4 + 8 = 13

```

Let's try with a bigger number:
```
Starting with 101101
- Reverse it to become 101101

There is a 1 in the ones column, so we start the equation with +1.
There is a 0 in the twos column, so we ignore it.
There is a 1 in the fours column, so we add 4 to the equation.
There is a 1 in the eights column, so we add 8 to the equation.
There is a 0 in the sixteens column, so we ignore it.
There is a 1 in the thirty twos column, so we add 32 to the equation.

After finishing with each digit, we can finalize our equation:
1 + 4 + 8 + 32 = 45

```

## How to convert a decimal to binary
Given 45, convert it to it's binary counterpart:
```
string convert()
{
    int input = 45;

    // Define a List<int> where all of the remainders will be stored.
    List<int> remainders = new List<int>();

    // Perform a while loop to continue running until input is 0.
    // For every iteration of this loop, input is going to be divided by 2.
    // However, before we divide it, we are going to log all of the remainders (1 or 0).
    while (input != 0)
    {
        // Find the remainder.
        // We are going to use the modul0 operation to find the remainder.
        int remainder = input % 2;

        // Add it to the list before doing anything.
        remainders.Add(remainder);

        // Continue the loop by dividing input by 2.
        input /= 2;
    }

    // At the end, when all of the remainders have been added to list, reverse it.
    List.Reverse(remainders);

    // Convert the list to a string, which will be the binary result.
    string binary = String.Join("", remainders.Select(x => x.toString()).ToList());
}
```