[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/ySCT0iTa)

# Lab One: Checkers Pieces
In this lab, you will explore a maintenance task that does not take advantage of patterns. The goals of this lab include
refreshing skills with Java and JavaFX and to encounter coding challenges that are addressed by introducing design patterns.

In checkers, pieces move diagonally, staying on the same color squares. Each move is to an empty square. When that square 
is adjacent, the piece moves just one square. If an adjacent square is occupied by an opponent’s piece and the square past 
that (in a straight line) is unoccupied, the piece can capture the opponent’s piece by jumping it. At the start of the game, 
all pieces are regular pieces, meaning they can only move towards the opponent’s side.

In this lab you will add support for kings. Once a piece reaches the opponent’s side of the board, the piece is “kinged” by 
placing a second checker on it. Kings can then move both forwards and backwards. This is the only difference; they must stay 
on the same color squares (moving diagonally) and can only move to an adjacent square or jump one opponent piece.


## The First Six Steps
The following steps add king pieces to the game. All changes in this lab should be to the file ```Piece.java```. 
- [*] Identify the place in the code where the type of piece is defined.
- [*] Add a boolean at that place to track whether a piece is a “king”.
- [*] Add an optional parameter to the Piece constructor that allows clients to create pieces as kings from the start. By default, pieces are not kings. As you do this, keep the DRY principle in mind!
- [*] Identify the place in the code where it determines that a black piece has reached the last row of the board.
- [*] Modify this code to identify when a red piece has reached the last row as it moves in the opposite direction across the board.
- [ ] When a piece reaches one of these positions, update the piece’s state to indicate it now represents a king.

### Solution to First Six Steps
The following solutions are listed below here for the steps that are listed above. These are changes in ```Piece.java```
1. Identify the place in the code where the type of piece is defined:
```
    public enum Type {
        RED, BLACK
    }
    private final Type type;
```
2. Add a boolean at that place to track whether a piece is a “king”.
```
    private boolean isKing;
```
3. Add an optional parameter to the Piece constructor that allows clients to create pieces as kings from the start. By default, pieces are not kings. As you do this, keep the DRY principle in mind!
```
    public Piece(Type type, int x, int y, boolean isKing) {
        this.type = type;
        this.x = x;
        this.y = y;
        this.isKing = isKing;
        ellipse = createEllipse();
        kingEllipse = createEllipse();
        kingEllipse.setVisible(false);
        reposition();
        BoardController.getSquare(x, y).placePiece(this);

    }
```
4. Identify the place in the code where it determines that a black piece has reached the last row of the board.
```
    private void move(Square square) {
        BoardController.getSquare(x, y).removePiece();
        placeOnSquare(square);
        BoardController.switchTurns();
        setActive(false);

        if(type.equals(Type.BLACK) && y == 0) {
            this.isKing = true;
            kingEllipse.setVisible(true);
            BoardController.setMessage("The Black Piece is now a King");
        } else if(type.equals(Type.RED) && y == 5) {
            this.isKing = true;
            kingEllipse.setVisible(true);
            BoardController.setMessage("The Red Piece is now a King");
        }
    }
```

5. Modify this code to identify when a red piece has reached the last row as it moves in the opposite direction across the board.
```
else if(type.equals(Type.RED) && y == 5) {
            this.isKing = true;
            kingEllipse.setVisible(true);
            BoardController.setMessage("The Red Piece is now a King");
       }
```

6. When a piece reaches one of these positions, update the piece’s state to indicate it now represents a king.
```
        if(type.equals(Type.BLACK) && y == 0) {
            this.isKing = true;
            kingEllipse.setVisible(true);
            BoardController.setMessage("The Black Piece is now a King");
        } else if(type.equals(Type.RED) && y == 5) {
            this.isKing = true;
            kingEllipse.setVisible(true);
            BoardController.setMessage("The Red Piece is now a King");
        }
```