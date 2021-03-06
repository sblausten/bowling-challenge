
Bowling Game
============
Project to implement the business logic for a single player bowling game in JavaScript.

## My approach
I decided to use a nested array to record frames and rolls on a scorecard.

Bonuses are added to the previous frame's array on the scorecard as extra elements so that each frame can easily be summed from the card when displaying totals on the front end.

I used a Game class to control core game logic like creating new frames and deciding when the game was finished. It also initializes all object instances and passes the scorecard through to each frame so that the frame can handle updating the scorecard.
(I was not sure whether it was better to get the frame to pass its scores back to Game so that game could update ScoreCard but decided that it added an extra layer of complexity for no apparent benefit at this stage except for reducing dependancy.)

I used a Frame class to implement the main play command from Game and return a random score for each roll using a Roll helper class.

I then used a ScoreCard class to keep track of each frame. The Frame class updates the score card after each roll so that the card will be able to keep the user interface up to date also.

The ScoreCard also contains and implements all the bonus logic for Strikes and Spares.

## To get a local copy:
```bash
git clone https://github.com/sblausten/bowling-challenge.git
cd bowling-challenge
```

### To run tests
```bash
npm i
open SpecRunner.html
```
If open command does not work on your machine, just copy the full path of the SpecRunner file into your browser's address bar.

## Things I'd like to do to extend
- Add a user interface
- Add some more edge case integration tests for end game scenarios.

## Features implemented
- [x] Play two rolls per frame
- [x] End a frame when I score 10 in first roll
- [x] Keep track of my score for each roll including skipped ones
- [x] Keep track of my score for each frame including bonuses
- [x] Add this frame to the last frame if it was a strike
- [x] Add the first roll to the last frame if it was a spare
- [x] End game after 10 frames
- [x] Continue game past 10 frames when the previous frame is a strike
- [x] End game after 13 frames if the last four frames are strikes.

## Rule details

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

![Ten Pin Score Example](images/example_ten_pin_scoring.png)
