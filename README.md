Sure! Let’s tackle this step by step.


---

a) UNIX Commands

1. List of users currently logged in:
```
who
```

or

```
w
```

2. Print the calendar of the current month and year:
```
cal
```



---

b) Shell Script to Compute Simple Interest and Compound Interest

Here’s a simple shell script:
```
echo "Enter Principal:"
read p
echo "Enter Rate of Interest:"
read r
echo "Enter Time (in years):"
read t

si=$(echo "scale=2; $p * $r * $t / 100" | bc)
ci=$(echo "scale=2; $p * (1 + $r / 100)^$t - $p" | bc -l)

echo "Simple Interest: $si"
echo "Compound Interest: $ci"
```

Save it as interest.sh, make it executable:

```
chmod +x interest.sh
```

Then run:

```
./interest.sh
```


---

c) C Program for Round Robin Scheduling

Here’s a C program to implement the Round Robin Scheduling algorithm:

```
#include <stdio.h>

int main() {
    int n, tq, bt[10], rt[10], t = 0, i;
    printf("Processes: ");
    scanf("%d", &n);

    printf("Burst times:\n");
    for (i = 0; i < n; i++) {
        scanf("%d", &bt[i]);
        rt[i] = bt[i];
    }

    printf("Time quantum: ");
    scanf("%d", &tq);

    int wt[10] = {0}, done;
    do {
        done = 1;
        for (i = 0; i < n; i++) {
            if (rt[i] > 0) {
                done = 0;
                if (rt[i] > tq) {
                    t += tq;
                    rt[i] -= tq;
                } else {
                    t += rt[i];
                    wt[i] = t - bt[i];
                    rt[i] = 0;
                }
            }
        }
    } while (!done);

    printf("P\tBT\tWT\tTAT\n");
    for (i = 0; i < n; i++)
        printf("P%d\t%d\t%d\t%d\n", i + 1, bt[i], wt[i], bt[i] + wt[i]);

    return 0;
}
```

Compile and run:

```
gcc round_robin.c -o round_robin
./round_robin
```

---

Let me know if you’d like any tweaks or explanations!

