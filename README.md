# mini-project-circular-linked-list

#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>

struct ts {
    char *color;
    struct ts *link;
};
typedef struct ts* TS;

TS getnode() {
    TS temp = (TS)malloc(sizeof(struct ts));
    if (temp == NULL) {
        printf("Memory not allocated\n");
        exit(0);
    }
    return temp;
}

TS init() {
    TS red = getnode();
    red->color = "Red";
    red->link = NULL;

    TS yellow = getnode();
    yellow->color = "Yellow";
    yellow->link = NULL;

    TS green = getnode();
    green->color = "Green";
    green->link = NULL;

    // Link the nodes in a circular manner
    red->link = yellow;
    yellow->link = green;
    green->link = red;

    return red; // Return the starting node
}

void simulation(TS start) {
    TS current = start;
    while (1) {
        printf("Traffic signal color is: %s\n", current->color);
        sleep(2); // Pause for 2 seconds to simulate the traffic light duration
        current = current->link; // Move to the next traffic signal
    }
}

int main() {
    TS start = init();
    simulation(start);
    return 0;
}

