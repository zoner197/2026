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

Below are important properties of the merged Pascal's Triangle.

An element in the merged Pascal's Triangle is the sum of all overlapping elements in that position.
Take row 2, element 2, denoted as ${{2}\choose{2}}$ from now on, as an example:
$$
\binom{2}{2}_{merged} = \binom{2}{2}_{triangle\space1} + \binom{2}{1}_{triangle\space2} + \binom{2}{0}_{triangle\space3} = 4
$$
For later use, a python function is created to find the value at any given row and element.
```python
# Function to find pascal value based on row number (n), element number (r), and number of triangles (tris, 4 by default)
def value(n, r, tris):
    num = 0
    for tri in range(0, tris):
        # Calculate n choose (r - tri) and add valid answers
        if 0 <= r - tri <= n:
            num += math.comb(n, r - tri)
    return num
```

To find the total number of elements in a row the row number, $n$, can be added to the number of triangles, 4.
$$
Total\space Elements = n + 4
$$
A python function is created for this too.
```python
# Calculate number of elements in row (n) using number of triangles (tris)
def total_row(n, tris):
    return n + tris
```

The sum of all elements is the number of paths to a row.
$$
Total\space Paths = \sum_{i=0}^{Total \space Elements} \binom{n_i}{k_i}
$$
The python function for this:
```python
# Calculate total paths using row (n) and triangles (tris)
def total_paths(n, tris):
    paths = 0
    for r in range(total_row(n, tris)):
        paths += value(n, r, tris)
    return paths
```

Using all the properties above, the probability of the ball landing in a certain bin can be calculated.
If the bin is treated as an element, then the formula to calculate the probability of the ball landing on a certain element can be used.
$$
P(element) = \frac{\binom{n}{k}}{Total \space Paths}
$$
Below is the python equivalent of this.
```python
# Find the probability of landing on a certain element assuming any starting element at n = 0
def total_probability(n, r, tris):
    return value(n, r, tris) / total_paths(n, tris)
```

This process has to be repeated for every bin, for which a python program has been created.
```python
import probability as prob

def bins(n, tris):
    bins = []
    
    for bin in range(prob.total_row(n, tris)):
        bins.append(prob.total_probability(n, bin, tris))
    return bins

if __name__ == "__main__":
    print(bins(4, 4))
```

The output:
```
[0.015625, 0.078125, 0.171875, 0.234375, 0.234375, 0.171875, 0.078125, 0.015625]
```

The probabilities can be read as:
Bin 0: 0.015265
Bin 2: 0.078125
...
Bin 7: 0.015625

## Part B: Assigning Values to Bins
To assign values to each bin and ensure the expected value is within $\pm5\%$ of $2000, the expected value formula is used with game values substituted in.
Let:

| Variable       | Meaning                               |
| -------------- | ------------------------------------- |
| $P_m$          | Probability of Multiplier bin         |
| $P_M$          | Probability of Max Prize bin          |
| $P_0$          | Probability of Min Prize bin          |
| $P_t$          | Probability of Try Again bin          |
| $P_1$ to $P_4$ | Probabilities of custom value bins    |
| $r_1$ to $r_4$ | Values of custom value bins           |
| $R$            | $$r_1P_1 + r_2P_2 + r_3P_3 + r_4P_4$$ |

$$
e = \sum xP(x)
$$
$$
e = (1.5 \times e_{redrop})P_m + 50000P_M + 0P_0 + e_{redrop}P_t + R
$$
$e_{redrop}$ needs to be calculated separately due to the change in values on a redrop.
$$
e_{redrop} = 0P_m + 0P_0 + 6000P_t + 50000P_M + R
$$
$$
e_{redrop} = 50000P_M + 6000P_t + R
$$
$e_{redrop}$ is substituted into $e$ and simplified, yielding:
$$
e = (1.5P_m + P_t)(50000P_M + 6000P_t + R) + 50000P_M + R
$$
Since all the expected value and probabilities are constants, the only value left to be determined is $R$, so it is made the subject and $e$ is replaced with 2000.
$$
\frac{2000 - (1.5P_m + P_t)(50000P_M + 6000P_t) - 50000P_M}{1.5P_m + P_t + 1} = R
$$
Through this formula, $R$ can be calculated.

However, to find individual values for the custom bins, arbitrary $r_1$ to $r_3$ values can be substituted into the following equation, leaving only $r_4$ to be solved.
$$
\frac{R - r_1P_1 - r_2P_2 - r_3P_3}{P_4} = r_4
$$
If $r_4$ is negative, different values need to be chosen.

To find usable bin values, a python program is made to pick random bin arrangements and $r_1$ to $r_3$ values. It then calculates $r_4$ using the above method to ensure the expected value remains within $\pm5\%$ of $2000. The values are also rounded to whole numbers so they can be used in a game show, which works because of the acceptable $\pm5\%$ error range.
```python
from distribution import bins as b
from random import seed, shuffle, randint

# Picking constant arbitrary seed for reproducibility
seed(67)

# Simple class to store data for each P and r_i
class P:
    def __init__(self, name, price, value = 0, bin_index = 0):
        self.name = name
        self.price = price
        self.value = value
        self.bin_index = bin_index

e = 2000

# Setting up bins
probability = b(4,4)

for bin_number, prob in enumerate(probability):
    probability[bin_number] = (bin_number, prob)

P_0 = P("Minimum", 0)
P_M = P("Maximum", 50000)
P_t = P("Try Again", 6000)
P_m = P("Multiplier", 0)
r_1 = P("Random 1", 0)
r_2 = P("Random 2", 0)
r_3 = P("Random 3", 0)
r_4 = P("Random 4", 0)
bin = [P_0, P_M, P_t, P_m, r_1, r_2, r_3, r_4]

# Function that shuffles the bins
def shuffle_bins():
    shuffle(probability)
    for i in range(len(probability)):
        bin[i].value = probability[i][1]
        bin[i].bin_index = probability[i][0]

# R = r_1P(r_1) + ... r_4P(r_4)
R = 0
# r_1, r_2, r_3, r_4 values
r_1_value = 0
r_2_value = 0
r_3_value = 0
r_4_value = -1
while R <= 0:
    # Shuffle bins until valid R
    shuffle_bins()

    # Calculate total of random bin (r_i) values
    R = (e - (1.5 * P_m.value)*(50000 * P_M.value + 6000 * P_t.value) - 50000 * P_M.value)/(1.5 * P_m.value + P_t.value + 1)

# Pick random r_1 to r_3 values and calculate r_4 to ensure target ev
while not (50000 >= r_4_value >= 0):
    r_1_value = randint(0, 50000)
    r_2_value = randint(0, 50000)
    r_3_value = randint(0, 50000)
    r_4_value = int(round((R - r_1_value * r_1.value - r_2_value * r_2.value - r_3_value * r_3.value)/r_4.value, 0))

r_1.price = r_1_value
r_2.price = r_2_value
r_3.price = r_3_value
r_4.price = r_4_value

# Function that returns the EV
def ev():
    R_dupe = r_1_value * r_1.value + r_2_value * r_2.value + r_3_value * r_3.value + r_4_value * r_4.value
    e_t = 6000 * P_t.value + 50000 * P_M.value + R_dupe
    e_m = 6000 * P_t.value + 75000 * P_M.value + 1.5 * R_dupe
    return e_t * P_t.value + e_m * P_m.value + 50000 * P_M.value + R_dupe

# Function that returns the bin index and value of each outcome
def bins():
    bin_values = {}
    for outcome in [P_0, P_M, P_t, P_m, r_1, r_2, r_3, r_4]:
        bin_values[outcome.name] = {
            "bin": outcome.bin_index,
            "value": outcome.price
        }
    
    return bin_values

if __name__ == "__main__":
    # Print results if running as program and not module
    print(f"R: {R}")
    for i in bin:
        print(f"{i.name}: \n\tbin: {i.bin_index + 1}\n\tprobability: {i.value}\n\tvalue: {i.price}")

    print(f"\nEV: {ev()}")
```

The output:
```
R: 545.0819672131148
Minimum: 
        bin: 1
        probability: 0.015625
        value: 0
Maximum: 
        bin: 8
        probability: 0.015625
        value: 50000
Try Again: 
        bin: 2
        probability: 0.078125
        value: 6000
Multiplier: 
        bin: 4
        probability: 0.234375
        value: 0
Random 1:
        bin: 6
        probability: 0.171875
        value: 789
Random 2:
        bin: 7
        probability: 0.078125
        value: 722
Random 3:
        bin: 5
        probability: 0.234375
        value: 1076
Random 4:
        bin: 3
        probability: 0.171875
        value: 587

EV: 2042.741455078125
```

## Part C: Finding The Best Slot
To find the slot with the highest average payout, the aforementioned expected value formula can be used.
$$
e = (1.5P_m + P_t)(50000P_M + 6000P_t + R) + 50000P_M + R
$$
However, the probabilities used are those skewed by a starting slot rather than the previously calculated general probabilities.
These can be found by calculating elements differently. Previously, elements were calculated as such:
$$\binom{2}{2}_{merged} = \binom{2}{2}_{triangle\space1} + \binom{2}{1}_{triangle\space2} + \binom{2}{0}_{triangle\space3} = 4$$
Calculating them with $k - k_{starting \space slot}$ instead of $k$ gives the total numbers of paths to that element from the starting slot chosen, for example slot 1:
$$
\binom{2}{2}_{merged} = \binom{2}{2 - 1}_{triangle\space1} + \binom{2}{1 - 1}_{triangle\space2} + \binom{2}{0 - 1}_{triangle\space3}
$$
But the last term $\binom{2}{0-1}_{triangle \space 3}$ is invalid, so the equation becomes:
$$
\binom{2}{2}_{merged} = \binom{2}{1}_{triangle\space1} + \binom{2}{0}_{triangle\space2} = 3
$$

The previous python functions are altered to return results modified by the starting slot.
```python
# Function to find value based on a start element
def paths_to(n, r, start):
    if 0 <= r - start <= n:
        return math.comb(n, r - start)
    return 0
```

```python
# Calculate total paths using row (n) and triangles (tris) given a starting element in n = 0 (start)
def total_paths_from_start(n, start, tris):
    paths = 0
    for r in range(total_row(n, tris)):
        paths += paths_to(n, r, start)
    return paths
```

```python
# Find the probability of landing on a certain element given a starting element at n = 0
def probability(n, r, start, tris):
    return paths_to(n, r, start) / total_paths_from_start(n, start, tris)
```

```python
# Function to find probability distribution based on starting slot

def bins(start):
    bins = []
    for bin in range(8):
        bins.append(p.paths_to(4, bin, start)/p.total_paths_from_start(4, start, 4))
    return bins
```

Additionally, a python program is made to calculate the expected value using starting slot and return the best one.

```python
import probability as p
import expected    as e

# Function to find probability distribution based on starting slot
def bins(start):
    bins = []

    for bin in range(8):
        bins.append(p.paths_to(4, bin, start)/p.total_paths_from_start(4, start, 4))

    return bins

# Precalculate bin probabilities for all starting slots
distributions = []
for slot in range(4):
    distributions.append(bins(slot))

def expected_value(distribution):
    bins = e.bins()
    
    base = bins["Maximum"]["value"] * distribution[bins["Maximum"]["bin"]] + bins["Random 1"]["value"] * distribution[bins["Random 1"]["bin"]] + bins["Random 2"]["value"] * distribution[bins["Random 2"]["bin"]] + bins["Random 3"]["value"] * distribution[bins["Random 3"]["bin"]] + bins["Random 4"]["value"] * distribution[bins["Random 4"]["bin"]]
    try_again = base + bins["Try Again"]["value"] * distribution[bins["Try Again"]["bin"]]
    multiplier = 1.5 * base + bins["Try Again"]["value"] * distribution[bins["Try Again"]["bin"]]
    ev = base + try_again * distribution[bins["Try Again"]["bin"]] + multiplier * distribution[bins["Multiplier"]["bin"]]

    return ev

def find_best():
    cache: list = []

    best: tuple = (0, 0)
    for slot, distribution in enumerate(distributions):
        ev = expected_value(distribution)
        if best[1] < ev:
            best = (slot, ev)
        elif best[1] == ev:
            print(f"Duplicate case: {slot}, {ev}")
        
        cache.append((slot, ev))
    
    return best, cache

if __name__ == "__main__":
    best, all_dist = find_best()
    print(f"{all_dist}\n\n{best}")
```

The output:
```
[(0, 1216.984375), (1, 919.7890625), (2, 938.5234375), (3, 4233.22265625)]

(3, 4233.22265625)
```

The best is slot 3, resulting in an expected value of approximately $4233.22.

# Evaluate
## Verification of Results
The results have been verified throughout the solving.

The bin probabilities add up to 1:
$$
0.015625 + 0.078125 + 0.171875 + 0.234375 + 0.234375 + 0.171875 + 0.078125 + 0.015625 = 1
$$

$r_4$ is calculated to be a number with many decimal digits that when substituted into the expected value equation with the other values, yields exactly $2000, so it is rounded to the nearest whole number for the game show. This could have introduced enough error to break the $\pm5\%$ range, justifying the expected value check after rounding, resulting in approximately $2042.74, which is within the range.

During calculations involving a starting slot, error checks are used in every python function to ensure there are no invalid values (e.g. $\binom{2}{-1}$).

> [!NOTE] Additions
> I verified the results in hundreds of ways that I didn't mention. I'll add them in if the word count permits.

## Considering Assumptions
The model yields an expected value of $2042.74, within the $\pm5\%$ range of the $2000 target. This result is highly reasonable under the 50% split assumption. Since the model assumes symmetry, the resulting distribution is a binomial expansion. If this assumption was removed, the probabilities would skew, moving the expected return outside the $\pm5\%$.

## Considering Observations
The observation that the board consists of merged Pascal's Triangles is validated by the symmetry of the results. The probabilities found for Bin 0 (0.0156) and Bin 7 (0.0156) are identical, closely aligning with the symmetry of the quincunx. Additionally, preventing infinite redrops was critical. Without this, the expected value formula would be recursive, leading to an unreasonable payout.

## Strengths
- Calculating overlapping triangles is susceptible to error, making the use of Python a strength, since the script computes values and ensures $\sum P(x) = 1$.
- Instead of guessing and checking bin values, a randomized algorithm is used to solve for $r_4$ ensuring that the $2000 target is met regardless of bin arrangement. This makes the model reusable, ensuring it can generate solutions for any values the game show may request in the future.
## Limitations
- The model assumes a frictionless environment, whereas in reality, the ball's initial velocity could lead to non-random outcomes, for example the ball favoring the center. The Multiplier Bin has a probability of 23.4%, meaning even a 2% change would significantly increase the expected value, costing the game show more than intended.
- To ensure they can be used on TV, the bin values were rounded to whole numbers. While this is necessary, it introduces some discrepancy between the target ($2000) and the expected value ($2042.74). Though this is within the acceptable $\pm5\%$ error range