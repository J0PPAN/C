#include <stdio.h>

struct Process {
    int pid;            // Process ID
    int arrival_time;   // Arrival Time
    int burst_time;     // Burst Time
    int priority;       // Priority (for Priority Scheduling)
};

// Function to calculate turnaround time and waiting time
void calculateTurnaroundTimeAndWaitingTime(struct Process processes[], int n) {
    int completion_time[n];
    int turnaround_time[n];
    int waiting_time[n];
    int total_waiting_time = 0;
    int total_turnaround_time = 0;

    // Calculate completion time for each process
    completion_time[0] = processes[0].burst_time;
    for (int i = 1; i < n; i++) {
        completion_time[i] = completion_time[i - 1] + processes[i].burst_time;
    }

    // Calculate turnaround time and waiting time for each process
    for (int i = 0; i < n; i++) {
        turnaround_time[i] = completion_time[i] - processes[i].arrival_time;
        waiting_time[i] = turnaround_time[i] - processes[i].burst_time;

        total_turnaround_time += turnaround_time[i];
        total_waiting_time += waiting_time[i];
    }

    // Calculate and print average turnaround time and waiting time
    double avg_turnaround_time = (double)total_turnaround_time / n;
    double avg_waiting_time = (double)total_waiting_time / n;

    printf("Process\tTurnaround Time\tWaiting Time\n");
    for (int i = 0; i < n; i++) {
        printf("P%d\t%d\t\t%d\n", processes[i].pid, turnaround_time[i], waiting_time[i]);
    }

    printf("Average Turnaround Time: %.2lf\n", avg_turnaround_time);
    printf("Average Waiting Time: %.2lf\n", avg_waiting_time);
}

int main() {
    int n;  // Number of processes
    printf("Enter the number of processes: ");
    scanf("%d", &n);

    struct Process processes[n];

    // Input process details
    for (int i = 0; i < n; i++) {
        processes[i].pid = i + 1;
        printf("Enter Arrival Time for P%d: ", i + 1);
        scanf("%d", &processes[i].arrival_time);
        printf("Enter Burst Time for P%d: ", i + 1);
        scanf("%d", &processes[i].burst_time);
        printf("Enter Priority for P%d (for Priority Scheduling): ", i + 1);
        scanf("%d", &processes[i].priority);
    }

    // Simulate FCFS (First-Come-First-Serve)
    printf("\nFCFS Scheduling:\n");
    calculateTurnaroundTimeAndWaitingTime(processes, n);

    // Simulate SJF (Shortest Job First)
    // Sort processes based on burst time (shortest first)
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (processes[j].burst_time > processes[j + 1].burst_time) {
                // Swap processes[j] and processes[j + 1]
                struct Process temp = processes[j];
                processes[j] = processes[j + 1];
                processes[j + 1] = temp;
            }
        }
    }
    printf("\nSJF Scheduling:\n");
    calculateTurnaroundTimeAndWaitingTime(processes, n);

    // Simulate Priority Scheduling
    // Sort processes based on priority (lower value is higher priority)
    for (int i = 0; i < n - 1; i++) {
        for (int j = 0; j < n - i - 1; j++) {
            if (processes[j].priority > processes[j + 1].priority) {
                // Swap processes[j] and processes[j + 1]
                struct Process temp = processes[j];
                processes[j] = processes[j + 1];
                processes[j + 1] = temp;
            }
        }
    }
    printf("\nPriority Scheduling:\n");
    calculateTurnaroundTimeAndWaitingTime(processes, n);

    // Simulate Round Robin Scheduling (preemptive) with time quantum of 4 units
    int time_quantum = 4;
    int remaining_burst_time[n];
    for (int i = 0; i < n; i++) {
        remaining_burst_time[i] = processes[i].burst_time;
    }
    int current_time = 0;
    int completed = 0;
    printf("\nRound Robin Scheduling:\n");
    while (completed < n) {
        for (int i = 0; i < n; i++) {
            if (remaining_burst_time[i] > 0) {
                if (remaining_burst_time[i] <= time_quantum) {
                    current_time += remaining_burst_time[i];
                    remaining_burst_time[i] = 0;
                    processes[i].burst_time = 0;
                } else {
                    current_time += time_quantum;
                    remaining_burst_time[i] -= time_quantum;
                }

                if (remaining_burst_time[i] == 0) {
                    completed++;
                    processes[i].burst_time = 0;
                    int turnaround_time = current_time - processes[i].arrival_time;
                    int waiting_time = turnaround_time - processes[i].burst_time;
                    printf("P%d\t%d\t%d\n", processes[i].pid, turnaround_time, waiting_time);
                }
            }
        }
    }

    return 0;
}
