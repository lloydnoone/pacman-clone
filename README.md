![ga_cog_large_red_rgb](https://cloud.githubusercontent.com/assets/40461/8183776/469f976e-1432-11e5-8199-6ac91363302b.png)

# pacman-clone

![image](https://user-images.githubusercontent.com/49749612/65820099-0528ce00-e21d-11e9-8ff8-f82e195a6171.png)

This was a project assigned to me by General Assembly during a software engineering immersive course. The purpose of the project was to solidify the skills we learnt in the first 4 weeks by putting them to use in a project of our choice.

It is a pacman clone in which i attempted to recreate the original games logic using common web development technologies.

## Built With

1. HTML5
2. CSS3
3. JavaScript
4. GitHub

## Deployment

The game is deployed on GitHub pages and it can be found here- https://lloydnoone.github.io/pacman-clone/

## Getting Started

Use the clone button to download the game source code. Open the index.html file in your browser and the game should start, if not check console for any issues. The assets used in this game are stored in the assets folder. They inlcude gifs, png files and fonts.

## Game Architecture

The goal in pacman is for the player to collect all the pips to complete the level. While doing this the player has to avoid ghosts. if the ghosts catch the player it is game over.

![](ezgif.com-video-to-gif.gif)

The ghosts have 3 modes of movement. 

* Chase
  > In chase the ghosts target pacman by comapring their postion to pacmans position on the gameboard in a staight line. This means they sometimes go the wrong way and is an intentional part of the game mechanics.
  
* scatter
  > In scatter, the ghosts will go to there respective corner and circle around until after a few seconds they put back in chase mode.
  
* frightened 
  > firghtened mode is activated when pacman eats the larger energizer dots. In this mode the ghosts take random turns and      move more slowly. This gives pacman a chance to chase down the ghosts and eat them for extra points.
  
A timer changes the ghosts from chase to scatter. because of this the ghosts attack in waves. The time remaining in each mode is remembered during frightened mode so that they go back to there previous state and carry on where they left off.

an example of the ghosts movement function-

```javascript
moveAmount(newIdx) {
      //remove cssClass from this cell before moving
      cells[this.ghostIdx].classList.remove(this.cssClass)
      //save reference to check next move
      this.previousIdx = this.ghostIdx
      // move the actual index by amount passed in
      this.ghostIdx = newIdx
      //place cssClass on new cell
      cells[this.ghostIdx].classList.add(this.cssClass)
    }
    checkNextIdx(nextIdx) {
      //check for wall and previous index
      return (cells[nextIdx].classList.contains('wall') === false && cells.indexOf(cells[nextIdx]) !== this.previousIdx)
    }
    checkTunnelMove() {
      if (this.ghostIdx === 200) {
        cells[this.ghostIdx].classList.remove(this.cssClass)
        this.ghostIdx = 218
        this.previousIdx = 219
      }
      if (this.ghostIdx === 219) {
        cells[this.ghostIdx].classList.remove(this.cssClass)
        this. ghostIdx = 201
        this.previousIdx = 200
      }
    }
    moveCloser() {
      //if ghost on the edge tile of a tunnel, transfer to other side
      this.checkTunnelMove()
      //get player and ghost coords
      const targetX = cells[this.targetIdx].getBoundingClientRect().left
      const ghostX = cells[this.ghostIdx].getBoundingClientRect().left
      const targetY = cells[this.targetIdx].getBoundingClientRect().top
      const ghostY = cells[this.ghostIdx].getBoundingClientRect().top
      // check up, if there is no wall and not previous position, move there
      if (this.checkNextIdx(this.ghostIdx - width) && ghostY > targetY) {
        //move up
        this.moveAmount(this.ghostIdx - width)
      } else if (this.checkNextIdx(this.ghostIdx + width) && ghostY < targetY) {
        //check down, if poss move there
        this.moveAmount(this.ghostIdx + width)
      } else if (this.checkNextIdx(this.ghostIdx - 1) && ghostX > targetX) {
        //check left, if poss move there
        this.moveAmount(this.ghostIdx - 1)
      } else if (this.checkNextIdx(this.ghostIdx + 1) && ghostX < targetX) {
        //check left, if poss move there
        this.moveAmount(this.ghostIdx + 1)
      }
    }
```

Upon eating all the pips, the player wins and is moved on to the next level. The stage is the same but the ghosts will now be moving faster. the ghosts speed will increase everytime the stage is cleared. 

## Wins and Blockers

The biggest blocker was  to create a ghost AI that was similair to the original pacman. I recreated this in much the same way by giving the ghosts the ability to change target tiles depending on which mode they are in. 

The part where i actually spent the most time and had the most difficulty was organizing the timers and intervals which control these states. They switch back and forth and are interupted by the frightened state and should resume where they left off. The functions handling this are complicated and need refactoring somehow.

A big win for me on this project was getting to grips with classes. Having dabbled a little with C++ games in the past i found this easy to pick up. Using classes felt more natural to me than making it without and this ability helped later on in the course whenever classes were needed.

## Future Features

The main future improvement for the project would be to expand on the level editor that i created for my own convenience. It would be a great idea to make this more user friendly and accesible to users. This would give a whole new feature where players could make there own stages for the game and save them.

## Key Learnings

The main thing i learnt on this project was actually time management in software development and prioritization. Being the first project on the course, it was the first chance I had the opportunity to manage my own time an workflow. I didnt struggle with this as i was quite confident on the project as a whole but I left the styling a bit late. This was because i should have stopped adding new features and concentrated on bug fixing earlier.

Another thing to note would be planning. I should have spent more time in the planning stage focusing on the actual architecture of the game before starting to code. I now appreciate this aspect more and spend more time with it.

![](leveleditor.gif)

## Author 

Lloyd Noone - portfolio: lloydnoone.com
