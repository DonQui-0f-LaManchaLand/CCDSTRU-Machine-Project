#### **SUBJECT TO CHANGE**

#### **IF THERE IS A (?) it means unsure about the translation (careful proofreading is needed!)**

#### Sets

C: positive integer less than 4 

- (1, 2, 3)

N: positive integer including 0 less than or equal to 16 

- (0, 1, 2, 3 , 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16)

M: C^2 or C x C

- (1, 2, 3) x (1, 2, 3)

|      |     |     |
| :--: | :-: | :-: |
| 1x1  | 1x2 | 1x3 |
|  2x1 | 2x2 | 2x3 |
|  3x1 | 3x2 | 3x3 |

V: {true , false}


#### System Variables

good = either true or false

go = either true or false

start = either true or false

over = either true or false

found = either true or false

val = 0-16

R, B, S, T, F are all in M ( M having more than or equal to this since this is a subset of M)

M = all positions

R = player 1 (?) - _I approve of this, initially I thought of calling it black or white, but_ 

B = player 2 (?)  _Red and Blue fit based on the initials_

S = idk - _assuming S and T are variables for positions, then I assume these_ 

T = idk    _variables are used to choose a position or validate (?)_

F = free positions (?) - I think they are


#### System Facts

Free positions(?) = all possible positions minus all occupied player 1(?) & player 2(?) positions 

Game over if 

- cardinality of f is 3 

- or value is more than or equal to 20

- or not start 

- And ( cardinality of R is positive & B = 0 or R is 0 and B is positive) 


#### System Initialization 

**good = false ****go = true ****start = true ****found = false**

**val = 0 ****R = ∅ ****B = ∅ ****S = ∅ ****T = ∅**

\



#### System States and Behavior 

**Remove(pos ∈ M)**

**go → (R = R − {pos})**

**¬go → (B = B − {pos})**

**S = S − {pos}**

**T = T − {pos}**

\


**If go is true then remove red(?)**

**If go is false then remove blue (?)**

**S & T are removed from the position** 

\


**Replace(pos ∈ M)**

**found = false**

**(go ∧ pos ∈ B) → (B = B − {pos} ∧ found = true)**

**(go ∧ pos ∈ R) → found = true**

**(go ∧ pos ̸∈ R) → (R = R ∪ {pos})**

**(¬go ∧ pos ∈ R) → (R = R − {pos} ∧ found = true)**

**(¬go ∧ pos ∈ B) → found = true**

**(¬go ∧ pos ̸∈ B) → (B = B ∪ {pos})**

**(found ∧ pos ̸∈ S) → (S = S ∪ {pos} ∧ found = false)**

**(found ∧ pos ∈ S ∧ pos ̸∈ T) → (T = T ∪ {pos} ∧ Expand(pos))**

1. **pre requisite to this : found is false**

2. **go to a position that is an element of B , where B is removed and found is changed to true** 

3. **go to a position that is element of  R and change found to true**

4. **go to a position that’s not an element of R and add that position to R**

5. **don’t go to a position within B and make found true** 

6.

\


**Expand(pos ∈ M)**

**(a, b) = pos**

**u, d, k, r ∈ M**

**u = (a − 1, b)**

**d = (a + 1, b)**

**k = (a, b − 1)**

**r = (a, b + 1)**

**Remove(pos)**

**(go) → Replace(u)**

**(¬go) → Replace(d)**

**Replace(k)**

**Replace(r)**

1. **Let (a, b) be coordinates of pos**

2. **Declare and Define variables:**

- **u = (a − 1, b); Assuming this is UP (?)**

- **d = (a + 1, b); Assuming this is DOWN (?)**

- **k = (a, b − 1); Assuming this is LEFT (?)**

- **r = (a, b + 1); Assuming this is RIGHT (?)**

| (a, b) |   0  |  1  |  2  |
| :----: | :--: | :-: | :-: |
|    0   | 1x1  | 1x2 | 1x3 |
|    1   |  2x1 | 2x2 | 2x3 |
|    2   |  3x1 | 3x2 | 3x3 |

\
\
\
\
\
\
\


3. **Create a function for remove(pos)**

4. **If go is true (1), then call Replace(u) // if(go == 1) Replace(u);**

5. **If go is false (0), then call Replace(d) // if(go == 0) Replace(d);**

6. **Always call Replace(k)**

7. **Always call Replace(r)**

\


**Update(pos ∈ M)**

**good = false**

**(pos ̸∈ S) → (S = S ∪ {pos} ∧ good = ¬good)**

**(¬good ∧ pos ∈ S ∧ pos ̸∈ T) → (T = T ∪ {pos} ∧ Expand(pos))**

1. **good = false (0);**

2. **If pos is not in S, then include pos to S and negate good (now true (1)).**

3. **If it’s true that pos is in S but not in T, then add pos to T and call Expand(pos).**

\


**NextPlayerMove(pos ∈ M)**

**(¬over ∧ start ∧ go) → (R = R ∪ {pos} ∧ S = S ∪ {pos} ∧ good = true)**

**(¬over ∧ start ∧ ¬go) → (B = B ∪ {pos} ∧ S = S ∪ {pos} ∧ good = true)**

**(¬over ∧ ¬start ∧ (go ∧ pos ∈ R ∨ ¬go ∧ pos ∈ B)) → (Update(pos) ∧ good = true)**

**(start ∧ |R| = 1 ∧ |B| = 1) → start = false**

**(¬over ∧ good) → (good = ¬good ∧ go = ¬go ∧ val = val + 1)**

**Initializations:**

**good = false ****go = true ****start = true ****found = false**

**val = 0 ****R = ∅ ****B = ∅ ****S = ∅ ****T = ∅**

1. **If it’s not over, but the game has started, and it’s a player’s turn, then add pos to R and add pos to S, and set good = true (does ‘good’ serve as a validation if a move is right?)**

2. **If it’s not over, but the game has started, and it’s the other player’s turn, then add pos to R and add pos to S, and set good = true**

3. **Oh damn**

\


**GameOver()**

**result ∈ {“R wins”, “B wins”, “draw”}**

**(over ∧ |R| > |B|) → result = “R wins”**

**(over ∧ |R| < |B|) → result = “B wins”**

**(over ∧ |R| = |B|) → result = “draw”**

**3 possible results** 

**If R has more slots than B r wins** 

**If R has less slots than B b wins**

**If they both have the same number of slots then it’s a draw**
and.
define next player move logic based on current state variables.
define game over conditions with results based on counts of R and B.
