**The Birthday Paradox Problem**

How many people are needed in a room to get a 50% chance of having two people with the same birthday?

Only 23 people.

- $V_{nr}$: total number of birthdays without repetitions
- $V_t$: total number of birthdays with repetition
- $P(A)$: Probability of not finding two people with the same birthday of 23 people

(a) $V_{nr} = \frac{n!}{(n-k)!} = \frac{365!}{(365-23)!}$

(b) $V_t = n^k = 365^{23}$

(c) $P(A) = \frac{V_{nr}}{V_t} \approx 0.492703$
