#include <stdio.h>
int main() {
    int frames[10], pages[30], temp[10];
    int no_of_frames, no_of_pages, flag, i, j, k, pos = 0, faults = 0;

    printf("Enter number of frames: ");
    scanf("%d", &no_of_frames);

    printf("Enter number of pages: ");
    scanf("%d", &no_of_pages);

    printf("Enter page reference string:\n");
    for(i = 0; i < no_of_pages; i++) {
        scanf("%d", &pages[i]);
    }

    // Initialize frames to -1 (empty)
    for(i = 0; i < no_of_frames; i++) {
        frames[i] = -1;
    }

    printf("\nPage\tFrames\n");
    for(i = 0; i < no_of_pages; i++) {
        printf("%d\t", pages[i]);
        flag = 0;

        // Check if page is already in frame
        for(j = 0; j < no_of_frames; j++) {
            if(frames[j] == pages[i]) {
                flag = 1; // HIT
                break;
            }
        }

        // If MISS (not found)
        if(flag == 0) {
            frames[pos] = pages[i];        // replace at current position
            pos = (pos + 1) % no_of_frames; // circular increment
            faults++;
        }

        // Print current frames
        for(k = 0; k < no_of_frames; k++) {
            if(frames[k] == -1)
                printf("- ");
            else
                printf("%d ", frames[k]);
        }
        printf("\n");
    }

    printf("\nTotal Page Faults = %d\n", faults);
    return 0;
}
