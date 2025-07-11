1.

```java
package org.example;

import java.util.ArrayList;
import java.util.HashMap;
import java.util.List;
import java.util.Map;

public class Main {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3, 2, 4, 5, 1, 1, 6, 3};

        List<Integer> fArr = topKFrequent(arr, 2);
        System.out.println(fArr);
    }

    protected static List<Integer> topKFrequent(int[] arr, int frequency) {
        if(arr == null) {
            throw new IllegalArgumentException("array can't be null");
        }
        if (frequency <= 0) {
           throw new IllegalArgumentException("frequency can't be zero or negative");
        }

        Map<Integer, Integer> freqMap = new HashMap<>();
        for (int num : arr) {
            freqMap.put(num, freqMap.getOrDefault(num, 0) + 1);
        }

        List<Integer> result = new ArrayList<>();
        for (Map.Entry<Integer, Integer> entry : freqMap.entrySet()) {
            if (entry.getValue() >= frequency) {
                result.add(entry.getKey());
            }
        }

        return result;
    }
}
```

TestCase

```java
package org.example;

import org.junit.jupiter.api.Test;

import java.util.Arrays;
import java.util.Collections;
import java.util.List;

import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertThrows;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class MainTest {

    @Test
    void testMultipleElementsMeetingFrequency() {
        int[] arr = {1, 2, 2, 3, 3, 3, 4, 4};
        List<Integer> expected = Arrays.asList(2, 3, 4);
        List<Integer> actual = Main.topKFrequent(arr, 2);
        assertTrue(actual.containsAll(expected) && expected.containsAll(actual));
    }

    @Test
    void testSingleElementMeetingFrequency() {
        int[] arr = {5, 5, 1, 2, 3};
        List<Integer> expected = Collections.singletonList(5);
        List<Integer> actual = Main.topKFrequent(arr, 2);
        assertEquals(expected, actual);
    }

    @Test
    void testNoElementMeetingFrequency() {
        int[] arr = {1, 2, 3, 4};
        List<Integer> expected = Collections.emptyList();
        List<Integer> actual = Main.topKFrequent(arr, 2);
        assertEquals(expected, actual);
    }

    @Test
    void testAllElementsMeetingFrequency() {
        int[] arr = {7, 7, 7, 7};
        List<Integer> expected = Collections.singletonList(7);
        List<Integer> actual = Main.topKFrequent(arr, 1);
        assertEquals(expected, actual);
    }

    @Test
    void testEmptyArray() {
        int[] arr = {};
        List<Integer> expected = Collections.emptyList();
        List<Integer> actual = Main.topKFrequent(arr, 1);
        assertEquals(expected, actual);
    }

    @Test
    void testNullArray() {
        Exception exception = assertThrows(IllegalArgumentException.class, () -> Main.topKFrequent(null, 1));
        assertEquals("array can't be null", exception.getMessage());
    }

    @Test
    void testFrequencyZero() {
        int[] arr = {1, 2, 3};
        Exception exception = assertThrows(IllegalArgumentException.class, () -> Main.topKFrequent(arr, 0));
        assertEquals("frequency can't be zero or negative", exception.getMessage());
    }

    @Test
    void testNegativeFrequency() {
        int[] arr = {1, 2, 2};
        Exception exception = assertThrows(IllegalArgumentException.class, () -> Main.topKFrequent(arr, -1));
        assertEquals("frequency can't be zero or negative", exception.getMessage());
    }


}

```



2.

```sql
SELECT
    customer_id,
    COUNT(*) AS order_count,
    SUM(order_amount) AS total_spent
FROM
    orders
WHERE
    order_date >= CURRENT_DATE - INTERVAL '30 days'
GROUP BY
    customer_id
HAVING
    COUNT(*) >= 2;
```

3.
[High Level Design](HighLevelDesign.md)