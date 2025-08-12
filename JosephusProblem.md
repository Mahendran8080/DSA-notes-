# Josephus Problem Solution

## Problem Description
The Josephus problem is a theoretical problem related to a certain elimination game:
- There are `n` people standing in a circle.
- Counting starts at a specified point and proceeds around the circle in a fixed direction.
- In each step, the `k-th` person is eliminated.
- The procedure is repeated with the remaining people until only one remains.

We need to find the position of the last remaining person.

## Solution Approach

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        int n = 6; // number of people
        int k = 5; // step count

        List<Integer> arr = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            arr.add(i);
        }

        int index = 0; // start position
        while (arr.size() > 1) {
            index = (index + k - 1) % arr.size(); // wrap around
            System.out.println("Element removed: " + arr.get(index));
            arr.remove(index); // remove person
        }

        System.out.println("Winner: " + arr.get(0));
    }
}
