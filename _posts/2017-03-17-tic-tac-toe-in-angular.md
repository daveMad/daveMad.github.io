---
layout: post
title: Tic Tac Toe Game in Angular
categories: [Angular]
tags : [angular]
---

> This is a simple Tic Tac Toe game written in Angular 2. You can find the source code [here](https://github.com/daveMad/TicTacToe-Angular2)

# Root Component
The project is again generate by angular-cli. I did not include routing in the app. There is only a root component, and a html & css file for it. I also did not touch *index.html*

## Logic

Let's have a look at our component, navigate to [*src/app/app.component.ts*](https://github.com/daveMad/TicTacToe-Angular2/blob/master/src/app/app.component.ts).

We have predefined some of our data and also we have this constructor:

```typescript
constructor(){
    this.init();
}
```

Normally you wouldn't call a function in Angular1 with a `this` statement, but in Angular 2 you gotta add `this` otherwise you will get error.

### boxClick() function

Then we have this **boxClick()** function, that takes a parameter with type **number**. Whenever user clicks on a box, this function will be triggered. The parameter number represents the grid number actually, can be between 0 and 9. 

- First, we update our empty boxes, removing the current one, **line 28**
- Secondly, we check if the current box is already marked as either *X* or *O*, **line 29**
    - If not, we mark the box with the player's choice either *X* or *O*, **line 32**
    - Then, we check if we have 3 marks as a straight or side by side, according to the game's rule, **line 34**
        - If so, we increase the score and reset the game then return
        - Else, we toggle the current turn
    - We also check if the game is a draw **line 44**
        - If so, we reset and alert the user
- Else if the box is marked, we alert the user **line 49**

### aiClick() function

**line 53** this function puts a mark to a randomly selected empty box, similar to the `boxClick()` function, - it redefines the empty boxes
- puts the Ai's mark to the selected box as either *X* or *O*
- Checks if Ai's won the game and resets if so
- Checks the game status if it's a draw

### processTheMove() function

As the name stands, we process either the player's or the Ai's move and check the result here

If you look at **line 15** we have a predefined array with some string elements. These elements represent the possible winning situations, for example, if either X or O stands in all of the `1 2 and 3`, then that means X wins the game.

So we simply check foreach possibility, if the marks at those grids are the same, then we alert a win situation.

The function has a parameter **weapon** representing either X or O. And if you look at the **line 88**, if that grid's mark is not the same as our *weapon*, we assign `false` to our boolean flag.

If our flag is not false, it simply means a win situation.

