**Introduction**

  _Overview of Course_
  * learn computational modes of thinking 
  * master the art of computational problem solving
  * make computers do what you want them to do 
  
  ___
  
  _Topics_
  
  * represent knowledge with _**data structures**_
  * _**iteration**_ and _**recursion**_ are computational metaphors 
  * _**organize**_ and _**modularize**_ systems using object classes and methods 
  * different classes of _**algorithms**_
  
  ___
  
  _What Does A Computer Do?_
  
  * Fundamentally:
    > * performs _**calculations**_ a billion calculations per second!
    > * _**remembers**_ results -- 100's of gigabytes of storage 
  * What kinds of calculations? 
    > * _**built-in**_ to the language 
    > * ones that _**you define**_ as the programmer 
    
  ___
  
  _Simple Calculations Enough?_
  
  * Searching the World Wide web
    > * 45 Billion Pages; 1,000 words/page; 10 operations/word
    > * Need 5.2 days to find something using simple operations
  * Playing Chess
    > * Average of 35 moves/setting; look ahead 6 moves; 1.8 Billion boards to check; 100 operations/choice
    > * 30 minutes to decide each move
  * Good algorithm design is also needed to accomplish a task!
  
  ___

  _Enough Storage?_
  
  * What if we could just precompute information and then look up the answer?
    > * Playing chess as an example
      > * Experts suggest 10^123 different possible games
        - Only 10^80 atoms in the observable universe (Not enough memory)
  ___
  
  _Are There Limits?_
  
  * Despite it's speed and size, a computer does have limitations 
    > * Some problems still too complex
      > * Accurate weather prediction at a local scale
      > * Cracking encryption schemes
    > * Some problems are fundamentally impossible to compute
      > * Predicting whether a piece of code will always halt with an answer for any input
  
**Knowledge**

_Types Of Knowledge_

* Computers know what you tell them
* _**Declarative Knowledge**_ is statements of fact
  > * there is candy taped to the underside of one chair
* _**Imperative Knowledge**_ is a recipe or "how to" 
  Computation
  > 1. face the students at the front of the room
  > 2. count up 3 rows
  > 3. start from the middle section's left side
  > 4. count to the right 1 chair
  > 5. reach under chair and find it
  
  ---

_A Numerical Example_

* square root of a numberx is y such that y*y = x
* recipe for deducing square root of number x 
  > 1. Start with a guess, g
  > 2. If g*g is close enough to x, stop and say g is the answer
  > 3. Otherwise make a new guess by averaging g and x/g
  > 4. Using the new guess, repeat process until close enough

| g             | g * g          | x/g           | (g+x / g) / 2 |
| -----------   | -----------    | -----------   | -----------   |
| 3             | 9              | 5.333         | 4.1667        |
| 4.1667        | 3.837          | 3.837         |  4.0035       |
| 4.0035        | 3.997          | 3.997         |  4.000002     |

---

_What Is Recipe?_

   1) sequence of simple steps
   2) flow of control process that specifies when each step is executed
   3) a means of determining when to stop
   
Steps 1+2+3 = an algorithm!

**Machines**



**Languages**

**Types**

**Variables**

**Operators and Branching**


