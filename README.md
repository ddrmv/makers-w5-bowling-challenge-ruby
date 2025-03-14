## Initial class design (it has been modified in development)
```
              ┌───────────────────────┐
              │ Scorecard             │
              │ ---------             │
              │ @player_name          │
              │ @frames = []          │
              │ #get_current_total    │
              └───────▲───────▲───────┘
                      │       │
                      │       │
┌─────────────────────┴─┐   ┌─┴─────────────────────┐
│ Frame                 ├───► LastFrame < Frame     │
│ -----                 │   │ ---------             │
│ @first_roll  (int)    │   │ @third_roll (int)     │
│ @second_roll (int)    │   │ #second_strike (bool) │
│ #strike?     (bool)   │   └───────────────────────┘
│ #spare?      (bool)   │
└───────────────────────┘
```
## Use
The user enters sequentially results for all rolls and receives display of the
current state of the full scorecard after each frame.

## Output
```
Frame 1, roll 1: 7
Frame 1, roll 2: 3
Volo
Frame  1 - | |7|/|   10
Frame  2 - | | | |
Frame  3 - | | | |
Frame  4 - | | | |
Frame  5 - | | | |
Frame  6 - | | | |
Frame  7 - | | | |
Frame  8 - | | | |
Frame  9 - | | | |
Frame 10 - | | | |
Frame 2, roll 1: 
```


```
Loki
Frame  1 - | |1|4|    5
Frame  2 - | |4|5|   14
Frame  3 - | |6|/|   29
Frame  4 - | |5|/|   49
Frame  5 - | |X| |   60
Frame  6 - | |0|1|   61
Frame  7 - | |7|/|   77
Frame  8 - | |6|/|   97
Frame  9 - | |X| |  117
Frame 10 - |2|/|6|  133
```

```
Loki
Frame  1 - | |X| |   30
Frame  2 - | |X| |   60
Frame  3 - | |X| |   90
Frame  4 - | |X| |  120
Frame  5 - | |X| |  150
Frame  6 - | |X| |  180
Frame  7 - | |X| |  210
Frame  8 - | |X| |  240
Frame  9 - | |X| |  270
Frame 10 - |X|X|X|  300
```

  

Bowling Challenge in Ruby
=================

* Feel free to use google, your notes, books, etc. but work on your own
* If you refer to the solution of another coach or student, please put a link to that in your README
* If you have a partial solution, **still check in a partial solution**
* You must submit a pull request to this repo with your code by 9am Monday week

## The Task

**THIS IS NOT A BOWLING GAME, IT IS A BOWLING SCORECARD PROGRAM. DO NOT GENERATE RANDOM ROLLS. THE USER INPUTS THE ROLLS.**

Count and sum the scores of a bowling game for one player. For this challenge, you do _not_ need to build a web app with a UI, instead, just focus on the logic for bowling (you also don't need a database). Next end-of-unit challenge, you will have the chance to translate the logic to Javascript and build a user interface.

A bowling game consists of 10 frames in which the player tries to knock down the 10 pins. In every frame the player can roll one or two times. The actual number depends on strikes and spares. The score of a frame is the number of knocked down pins plus bonuses for strikes and spares. After every frame the 10 pins are reset.

As usual please start by

* Forking this repo

* Finally submit a pull request before Monday week at 9am with your solution or partial solution.  However much or little amount of code you wrote please please please submit a pull request before Monday week at 9am. 

___STRONG HINT, IGNORE AT YOUR PERIL:___ Bowling is a deceptively complex game. Careful thought and thorough diagramming — both before and throughout — will save you literal hours of your life.

## Focus for this challenge
The focus for this challenge is to write high-quality code.

In order to do this, you may pay particular attention to the following:
* Using diagramming to plan your approach to the challenge
* TDD your code
* Focus on testing behaviour rather than state
* Commit often, with good commit messages
* Single Responsibility Principle and encapsulation
* Clear and readable code

## Bowling — how does it work?

### Strikes

The player has a strike if he knocks down all 10 pins with the first roll in a frame. The frame ends immediately (since there are no pins left for a second roll). The bonus for that frame is the number of pins knocked down by the next two rolls. That would be the next frame, unless the player rolls another strike.

### Spares

The player has a spare if the knocks down all 10 pins with the two rolls of a frame. The bonus for that frame is the number of pins knocked down by the next roll (first roll of next frame).

### 10th frame

If the player rolls a strike or spare in the 10th frame they can roll the additional balls for the bonus. But they can never roll more than 3 balls in the 10th frame. The additional rolls only count for the bonus not for the regular frame count.

    10, 10, 10 in the 10th frame gives 30 points (10 points for the regular first strike and 20 points for the bonus).
    1, 9, 10 in the 10th frame gives 20 points (10 points for the regular spare and 10 points for the bonus).

### Gutter Game

A Gutter Game is when the player never hits a pin (20 zero scores).

### Perfect Game

A Perfect Game is when the player rolls 12 strikes (10 regular strikes and 2 strikes for the bonus in the 10th frame). The Perfect Game scores 300 points.

In the image below you can find some score examples.

More about ten pin bowling here: http://en.wikipedia.org/wiki/Ten-pin_bowling

![Ten Pin Score Example](images/example_ten_pin_scoring.png)
