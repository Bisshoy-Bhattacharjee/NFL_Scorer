# NFL_Scorer

#include <stdio.h>
#include <stdlib.h>

void print_combinations(int score) {
    if (score == 0) {
        printf("0 TD + 2pt, 0 TD + FG, 0 TD, 0 3pt FG, 0 Safety\n");
        return;
    }

    for (int td = 0; td <= score / 6; td++) {
        for (int fg = 0; fg <= score / 3; fg++) {
            for (int safety = 0; safety <= score / 2; safety++) {
                for (int td_2pt = 0; td_2pt <= (score - (td * 6 + fg * 3 + safety * 2)) / 8; td_2pt++) {
                    for (int td_fg = 0; td_fg <= (score - (td * 6 + fg * 3 + safety * 2 + td_2pt * 8)) / 7; td_fg++) {
                        int remaining_score = score - (td * 6 + fg * 3 + safety * 2 + td_2pt * 8 + td_fg * 7);
                        if (remaining_score == 0) {
                            printf("%d TD + 2pt, %d TD + FG, %d TD, %d 3pt FG, %d Safety\n", td_2pt, td_fg, td, fg, safety);
                        }
                    }
                }
            }
        }
    }
}

int main() {
    int score;

    while (1) {
        printf("Enter 0 or 1 to STOP\n");
        printf("Enter the NFL score: ");
        scanf("%d", &score);

        if (score <= 1) {
            break;
        }

        printf("Possible combinations of scoring plays:\n");
        print_combinations(score);
    }

    return 0;
}
