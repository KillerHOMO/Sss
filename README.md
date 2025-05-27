Sure! Let’s tackle this step by step.


---

a) UNIX Commands

1. List of users currently logged in:

who

or

w


2. Print the calendar of the current month and year:

cal




---

b) Shell Script to Compute Simple Interest and Compound Interest

Here’s a simple shell script:

#!/bin/bash

echo "Enter Principal amount:"
read p

echo "Enter Rate of Interest:"
read r

echo "Enter Time (in years):"
read t

# Simple Interest
si=$(echo "scale=2; $p * $r * $t / 100" | bc)
echo "Simple Interest: $si"

# Compound Interest
# Using the formula: CI = P * ((1 + r/100)^t - 1)
amount=$(echo "scale=2; $p * (1 + $r / 100)^$t" | bc -l)
ci=$(echo "scale=2; $amount - $p" | bc)
echo "Compound Interest: $ci"

Save it as interest.sh, make it executable:

chmod +x interest.sh

Then run:

./interest.sh


---

c) C Program for Round Robin Scheduling

Here’s a C program to implement the Round Robin Scheduling algorithm:

#include <stdio.h>

int main() {
    int i, n, time, remain, temps = 0, time_quantum;
    int wait_time = 0, turnaround_time = 0, at[10], bt[10], rt[10];
    
    printf("Enter total number of processes: ");
    scanf("%d", &n);
    remain = n;
    
    for(i = 0; i < n; i++) {
        printf("Enter Arrival Time and Burst Time for Process %d: ", i+1);
        scanf("%d %d", &at[i], &bt[i]);
        rt[i] = bt[i];
    }
    
    printf("Enter Time Quantum: ");
    scanf("%d", &time_quantum);
    
    printf("\nProcess\t|Turnaround Time|Waiting Time\n");
    
    for(time = 0, i = 0; remain != 0; ) {
        if(rt[i] <= time_quantum && rt[i] > 0) {
            time += rt[i];
            rt[i] = 0;
            temps = 1;
        }
        else if(rt[i] > 0) {
            rt[i] -= time_quantum;
            time += time_quantum;
        }
        
        if(rt[i] == 0 && temps == 1) {
            remain--;
            printf("P[%d]\t|\t%d\t|\t%d\n", i+1, time - at[i], time - at[i] - bt[i]);
            wait_time += time - at[i] - bt[i];
            turnaround_time += time - at[i];
            temps = 0;
        }
        
        if(i == n-1)
            i = 0;
        else if(at[i+1] <= time)
            i++;
        else
            i = 0;
    }
    
    printf("\nAverage Waiting Time: %.2f", (float)wait_time/n);
    printf("\nAverage Turnaround Time: %.2f\n", (float)turnaround_time/n);
    
    return 0;
}

Compile and run:

gcc round_robin.c -o round_robin
./round_robin


---

Let me know if you’d like any tweaks or explanations!

