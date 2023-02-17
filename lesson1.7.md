# Lesson 1.7 - Hexadecimal Number System
Hexadecimal is a number system that operates with base-16. Although it can be confusing, it is superior to base-10 in the sense that we can represent larger numbers with less digits.

![hexadecimal-chart](https://cdn1.byjus.com/wp-content/uploads/2021/09/Hexadecimal-Number-System-Table.png)
sourced from - https://byjus.com/maths/hexadecimal-number-system/

## How to convert from decimal (base-10) to hexadecimal
Given 42069, convert it to hexadecimal:
```java
public static void main(String[] args)
{
    int decimal = 42069;
    String hexadecimal = convert(decimal);
    System.out.printf("Decimal - %d, Hexadecimal - %s", 
        decimal, hexadecimal);
}

private static String convert(int decimal)
{
    List<String> converted = new ArrayList<String>();

    while (decimal > 0)
    {
        int remainder = decimal % 16;
        converted.add(find(remainder));

        decimal /= 16;
    }

    Collections.reverse(converted);

    return String.join("", converted);
}

private static String find(Integer decimal)
{
    Map<Integer, String> charMap = new Map<Integer, String>();
    charMap.put(10, "A");
    charMap.put(11, "B");
    charMap.put(12, "C");
    charMap.put(13, "D");
    charMap.put(14, "E");
    charMap.put(15, "F");

    if (charMap.containsKey(decimal))
        return charMap.get(decimal);
    
    return decimal.toString();
}
```

This can of course be written out like this:
```
Our original value: 42069

42069 / 16 = 2629 rem 5
2629 / 16 = 164 rem 5
164 / 16 = 10.25 rem 4
10.25 / 16 = 0.64 rem 10.25 (A)

Once we find all of our remainders, we collect and reverse them to find our hexadecimal value: A, 4, 5, 5

Therefore, 42069 in hexadecimal is A455
```

## How to convert from hexadecimal to decimal (base-10)
Given A455, convert it to a decimal:
```java
public static void main(String[] args)
{
    String hexadecimal = "A455";
    int decimal = convert(hexadecimal);
    System.out.printf("Hexadecimal - %s, Decimal - %d", 
        hexadecimal, decimal);
}

private static int convert(String hexadecimal) throws Exception
{
    String[] split = hexadecimal.split("");
    reverse(split);

    int converted = 0;
    for (int i = 0; i < split.length(); i++)
    {
        if (i == 0)
        {
            converted += 
                Integer.parseInt(find(split[i]));

            continue;
        }

        converted += Integer.parseInt(find(split[i])) * Math.pow(16, i);
    }

    return converted;
}

private static int find(String hexadecimal)
{
    Map<String, Integer> charMap = new HashMap<String, Integer>();
    charMap.put("A", 10);
    charMap.put("B", 11);
    charMap.put("C", 12);
    charMap.put("D", 13);
    charMap.put("E", 14);
    charMap.put("F", 15);

    if (charMap.containsKey(hexadecimal))
        return charMap.get(hexadecimal);
    
    return decimal.toString();
}
````

This can be written out like:
```
Our original value: A455

1. Going from left to right, right out each digit into an equation like this:
x(5) + x(5) + x(4) + x(A[10]).

2. Now, if we think of it as a for loop, i would increase with each iteration. Therefore, we are going to replace the x's with Math.pow(16, i) - like so:
[Math.pow(16, 0) x 5] + [Math.pow(16, 1) x 5] + [Math.pow(16, 2)] + [Math.pow(16, 3) x A (10)]

3. Re-write the equation so we can use simple algebra to solve it (since 16^0 is 1, just start with 5):
5 + 16^1(5) + 16^2(4) + 16^3(10)

4. Finalize our equation:
5 + 80 + 1024 + 40960 = 42069

5. Bask in the glory of you now being a HEX god.
```