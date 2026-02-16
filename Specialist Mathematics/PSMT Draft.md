# Title Page \[PLACEHOLDER]
> [!TODO]

![[Pasted image 20260214162407.png]]
> "We're cooked."
> \- Sun Tzu, The Art of War

Name: Kavii Sompura
Student Number: 165

# Contents
> [!TODO]

# Appendix
> [!TODO]
> Place all code here

# Abstract
> [!TODO]
> Shorten and convert dot points into paragraphs where appropriate.

## Game Summary
The Wall is a game show where contestants answer general knowledge questions and get to drop a ball into a quincunx if correct. They can pick from one of four slots to drop the ball from, and it can fall into one of eight bins.
![[Pasted image 20260214182910.png]]
*Figure 1: The Wall Diagram*

## Values
Each bin contains one of the following:
- Minimum Prize: $0
- Maximum Prize: $50,000
- Try Again: Contestant can redrop. On the redrop, the Try Again value is replaced with $6000.
- Multiplier: Contestant can redrop, but all bin values except Try Again and Multiplier are multiplier by 1.5. Try Again remains $6000, while Multiplier is replaced with $0.
- The four remaining bins contain different prize values between $0 and $50,000.

## Aim
Through the use of Python and combinatorics, this investigation aims to:
1. Analyze the probability distribution of all bins.
2. Assign values to each bin that are within $\pm5\%$ of the Expected Return ($2000).
3. Find the best slot for contestants to drop the ball into.

# Formulate
> [!TODO] Note
> Fix dog water reasoning.
## Observations
- Contestants cannot get a redrop within a redrop due to the Try Again and Multiplier values being replaced. This is essential, because calculations would be recursive otherwise, leading to infinite expected values.
- The shape of the quincunx is four merged Pascal's Triangles, allowing for probability and path calculations through combinatorics.
- The quincunx is a closed system where the ball cannot exit the peg area, meaning the sum of all bin probabilities is 1, permitting verification of probabilities.
## Assumptions
- On a multiplier redrop, the Try Again value is not multiplied. This is an essential assumption to ensure that the expected value remains constant.
- The pegs are evenly spaced, the ball cannot bounce to other pegs on the same or higher row, and friction/air resistance are negligible, so there is exactly a 50% chance of the ball falling either side. This assumption is crucial for the use of Pascal's Triangle and combinatorics in the bin probability calculations.
- The player picks their slot at random, so a $\frac{1}{4}$ probability can be assumed for each slot. This is critical because it simplifies bin probability distribution calculations to combinatorics rather than psychology.

# Mathematical Translation
Combinatorics, specifically relating to Pascal's Triangle, is required to complete the task. Pascal's triangle, as shown in Figure 2, is a triangle where an element is equal to the sum of the two elements diagonally above. Note that each element corresponds to the number of paths to it from the apex.

![[PSMT Draft.jpg]]
*Figure 2: Traditional Pascal's Triangle*

To find a particular element in Pascal's Triangle without drawing it, the combination formula can be used.
$$
{{n}\choose{k}} = \frac{n!}{k!(n-k)!}
$$
Where $n$ is the row number from top to bottom and $k$ is the element number from left to right, both starting from 0.

To find the amount of money that contestants can earn from a particular bin arrangement, the expected value formula can be used.
$$
e = \sum x P(x)
$$
Where $e$ is the expected value, $x$ is the payout of an outcome, and $P(x)$ is the probability of outcome $x$.

# Solve
## Part A: Finding Bin Probabilities
The shape of The Wall game is that of four merged pascal's triangles, meaning that many of the patterns in a traditional Pascal's Triangle still apply.

![[PSMT Draft.jpeg]]
*Figure 3: Merged Pascal's Triangles*

An element in the merged Pascal's Triangle is the sum of all overlapping elements in that position.
Take row 2, element 2, denoted as ${{2}\choose{2}}$ from now on, as an example:
$$
\binom{2}{2}_{merged} = \binom{2}{2}_{triangle\space1} + \binom{2}{1}_{triangle\space2} + \binom{2}{0}_{triangle\space3}
$$
