#include <stdio.h>

int main() {
    int n, i;

    printf("Enter number of processes:\n");
    scanf("%d", &n);

    char pid[n][5];
    int at[n], bt[n], ct[n], wt[n], tat[n];

    printf("Enter PID Arrival Time Burst Time:\n");
    for(i = 0; i < n; i++) {
        scanf("%s %d %d", pid[i], &at[i], &bt[i]);
    }

    int time = 0;
    float total_wt = 0, total_tat = 0;

    for(i = 0; i < n; i++) {

        if(time < at[i]) {
            time = at[i];   // CPU waits if process arrives later
        }

        ct[i] = time + bt[i];
        time = ct[i];

        tat[i] = ct[i] - at[i];
        wt[i] = tat[i] - bt[i];

        total_wt += wt[i];
        total_tat += tat[i];
    }

    printf("\nWaiting Time:\n");
    for(i = 0; i < n; i++) {
        printf("%s %d\n", pid[i], wt[i]);
    }

    printf("\nTurnaround Time:\n");
    for(i = 0; i < n; i++) {
        printf("%s %d\n", pid[i], tat[i]);
    }

    printf("\nAverage Waiting Time: %.2f\n", total_wt/n);
    printf("Average Turnaround Time: %.2f\n", total_tat/n);

    return 0;
}
