---
layout: default
title: chisquare
nav_exclude: true
---

An algorithm is just a series of steps, a recipe if you will. Each individual step is just a tiny action. In this exercise, we're going to turn a statistical formula - the Chi-Square test of association - into a series of little steps so that you can see what is going on. (In math, 'chi square' looks like a fancy X with a small 2.)

Let's say you've been doing a survey of a river valley, and you have noticed that some sites have bronze axe heads. You wonder if there is any association between sites with bronze axe heads, and where those sites are - close by the river, and further up in the hills. You can easily imagine explanations for _either_ option, so it would be nice to know which one is more statistically _plausible_.

You gather the data, and make a 2 x 2 'contingency table', where you count your data:

||riverside|non-riverside|
|--|--|--|
|bronze|160|150|
|non-bronze|200|130|

To look at this, you can't really tell if there is any association at play. So we will work out what a random distribution would look like, and by comparing what we observe with what we expect (what things would look like if there were no associations) we can figure out whether or not there's an association, how strong that association is, and what exactly is associated.

> A word about Spreadsheets and how they work

We're going to use Excel. A spreadsheet is a grid of columns and rows. Each column is named - A, B, C... all the way up to ZZ; and each row is numbered, 1, 2, 3, all the way down to something like 66540. That's a lot of data!. Each cell can hold a number, and since each cell has an address - A1 is in the top left corner, B1 is right beside it - we can write a formula in another cell that says 'take the value in A1 and multiply it by the value in B1'. When a formula works, you only see the value that it calculates; you have to move the cursor onto the cell and then you'll see the formula itself up in the editor bar above the spreadsheet. Every formula in Excel starts with a = sign: `=a1*b2` is the formula for multiplying whatever's in A1 against whatever's in B2. Certain common calculations or 'functions' can be used in a formula. `=AVERAGE(A1:A10)` will add up every number in A1, A2, A3... all the way to A10, and divide by the count of numbers added together to give an average. The : sign between the two cell addresses means 'range', ie, the range of values from A1 to A10. Other common functions are `MODE` and `MEDIAN` and `SUM` and `SQRT`.

Google sheets and other software (Apple Numbers, LibreOffic Calc etc) work the same way, even if the exact function name can sometimes be different.

## Set up our observed 'contingencies', ie, the data that we're exploring

**Step 1** Open excel, and in cell B1 write 'riverside'. In C1 write 'non-riverside. In A2 write 'bronze'. Complete the table.

**Step 2** Now we're going to calculate the SUM for each column and each row. In cell B4, write: **=sum(B2:B3)**
The value that displays should be '360', right? **Now what should go in cell C4?**

**Step 3** With column totals calculated, we can do row totals. We use the SUM command again. In cell D2, write: **=sum(b2:c2)** . You've just defined a range that goes along the row, and asked Excel to add up every value. You should see 310 as a result. **What should go into cell D3?**

**Step 4** The final step in setting up our contingency table is to add up all of our observations so we know the total count. Figure out the range for which you want to add every value together, and use that with the **sum** command. Put that formula in cell **d4**

You should see something like this:
||A|B|C|D|
|--|--|--|--|--|
|1|observed|riverside|non-riverside|
|2|bronze|160|150|310|
|3|non-bronze|200|130|330|
|4||360|280|640|

## Now to figure out the 'expected' values

To figure out the expected values for each cell in the contingency talbe (eg, how many sites, if everything were random, would be riverside AND have bronze axe heads) we calculate FOR EACH CELL 'row total x column total / grand total'.

So for riverside|bronze, that would be =310 * 360 / 640
for riverside|non-bronze, that would be =**330** * 360 / 640 (see that we used the different row total there?)

For non-riverside|bronze, that would be =310 * 280 / 640
For non-riverside|non-bronze, that would be =33 * 280 / 640.

You can write that as a formula in each cell; just remember to put the = sign in front (eg: ```=310*360/640)```

Alternatively, since you know the cell addresses for your original data, you could do this; note that I create our 'expected' table right underneath the 'observed' one:

||A|B|C|D|
|--|--|--|--|--|
|5|expected|riverside|non-riverside|
|6|bronze|=B4*D2/D4|=C4*D2/D4|=sum(b6:d6)|
|7|non-bronze|B4*D3/D4|||
|8|||||

why would you want to do this? Well, if you change a value in the original 'observed' table, any cells that depend on that one will **automatically** recalculate. That's a handy trick.

You should be able to complete this table on your own.

## Comparing the observed and expected values, and then adding up the differences.

We take each observation, and subtract the expected value. Ie, the first cell 160 - 174.375 = -14.375

We square the result, ie -14.375 * -14.375 = 206.640625

We divide _that_ result by the original expected value. 206.640625 / 174.375 = 1.185035842

We **don't** have to do any fancy calculations, because each individual calculation is just a small adjustment to the previous step. In the table below, each column shows what change we've done as we move from observed -> expected, observed - expected, the square of _that_ value, and then in the last step by dividing by the expected value.

The final step will be to add up all of the values in that final column: these are the sum of all squared differences weighted by expectation. **This total is your Chi-Square test statistic.**

Make a new table underneath the Expected table, and follow the patterns to complete the formula:

||A|B|C|D|E|F|
|--|--|--|--|--|--|--|
|9|observed|expected|O-E|(O-E)^2|(O-E)^2/E
|10|=b2|=b6|=a10-b10|=c10^2|=d10/b10
|11|=c2|=c6|||
|12|=b3|=b7|||
|13|=c3|=c7|||
|14||||||=sum(e10:e13)|

That final sum is your chi-square value, your chi-square statistic! Congratulations! Save your work!

## Great! What does it mean?

Statisticians have worked out that if you are working with a 2 x 2 contingency table (like we are), the the 'degrees of freedom' for that table is 1. Basically, they have worked out what the values would have to be, given more and more complex data, for a chi-square statistic to show a statistically significant difference rather than random chance alone (i.e., to reject the null hypothesis).

These benchmark numbers are called **critical values**. 

Because more complex tables have more cells (and therefore naturally accumulate larger sum totals), the threshold required to prove a pattern is "real" gets higher as the degrees of freedom increase. 

For our **2 × 2 table (df=1))**, statisticians calculated that under the standard 95% confidence level (alpha = 0.05):

* **The threshold is 3.84.**
* If your calculated chi square is **less than 3.84**, the difference could easily be random noise—you **fail to reject the null hypothesis**.
* If your calculated chi square is **greater than 3.84**, there is less than a 5% chance this happened by accident—you **reject the null hypothesis**.

The 'null hypothesis' is: "there is no association between bronze axes and location". So... what's our chi-square statistic, and is it greater than 3.84? 

In Excel, instead of looking up a table to read the critical value, you can run this formula: 

```excel
=CHISQ.DIST.RT(chi_square_value, df)   
```

ie, you replace 'chi_square_value' with the cell address of your statistic, and replace 'df' with your actual degrees of freedom. If you've been following my guide, your chi square value is in cell F14, and df is 1, thus: ```=CHISQ.DIST.RT(f14, 1)```. This returns the **probability**. If that number is **less than** 0.05 you reject the null hypothesis and conclude that the observed counts differ significantly from what would be expected by chance. 

### Why is df = 1 for a 2 × 2 table?

Think of it like a Sudoku puzzle. If you fix the row totals and column totals of your 2 × 2 table, **you only have the freedom to choose a number for a single cell**. Once you write down that one number, the other three cells are mathematically locked in place to satisfy the totals. Hence, you only have **1 degree of freedom**.

## Ok, we have a result, but what does it mean?

First of all, if we have 'rejected the null hypothesis' it does mean that there's a good chance that there is some kind of association. But we're not done yet.

A common mistake is thinking a massive Chi-Square number means a massive real-world effect. It doesn’t. 

Because Chi-Square multiplies everything by sample size ($N$), **if you simply collected 10 times more data, your Chi-Square statistic will become 10 times bigger**, even if the underlying pattern hasn’t changed by a single percent!

* **Chi-Square** only answers: *"Are we sure this isn't random luck?"*
* **Phi and Cramer's V** answer: *"Regardless of sample size, how strong is the actual relationship?"*

---

### 1. The Phi Coefficient: For 2 × 2 Tables

Statisticians realized they could strip the sample size (N) back out of the Chi-Square statistic to measure the pure strength of the connection. This is called 'phi'.

  * It works just like a correlation coefficient (r):
  * It scales between **$0$** (no relationship whatsoever) and **1** (a perfect, 100% predictive relationship).
  * If calculated directly from the raw counts, it can even have a **+ or - sign**, telling you which direction the relationship points.


### How to Calculate 

Remember that our contingency table is in cells **`B2:C3`**:

| | Column 1 | Column 2 |
|---|:---:|:---:|
| **Row 1** | **B2** | **C2** |
| **Row 2** | **B3** | **C3** |

#### Option A: If you already have your chi square value (e.g., in cell `D5`)
To get **Cramer’s V** (Strength: 0 to 1):

```excel
=SQRT(f14 / SUM(B2:C3))
```

(Notice that we're following the order of operations. We sum first, and then divide chi square by that value)


#### Option B: Calculate Signed Phi directly from the table (Direction + Strength: -1 to +1)
To get both the direction and the strength without even needing chi square:

```excel
=(B2*C3 - C2*B3) / SQRT((B2+C2) * (B3+C3) * (B2+B3) * (C2+C3))
```

If Phi is **postive** it means that the relationship implied by reading the original contingency table diagonal from top left to bottom right is the key relationship. Here, that would mean that Bronze Axeheads are associated with Riverside locations, and non-bronze with non-riverside.

If Phi is **negative** it means that the relationship implied by reading the original contingency table diagonal from top right to bottom left is the key relationship: bronze axeheads are associated with non-riverside locations, and non-bronze with riverside.

Unlike p-values (which we saw back when we were trying to decide whether or not the chi square statistic was meaning), which are either significant or not, Cramer’s V and phi are interpreted by benchmarks:

| Value of V or phi | Real-World Meaning |
| :---: | :--- |
| **approx 0.10$** | **Weak:** A slight tendency, but lots of noise. |
| **approx 0.30$** | **Moderate:** A clear, noticeable relationship. |
| **greater than or equal to 0.50$** | **Strong:** A massive, defining pattern. |

So.... what did you find? Can you write it up in a paragraph or two?


## The End

- you've learned to use a spreadsheet
- you've broken a statistical test down into a series of steps to figure out the result
- you've done that by using cell addresses so that if your data changes you only have to update one small table and the entire thing will recalculate - this is a kind of programming!
- you've evaluated the likelihood of an association between archaeological variables, and you've tested the strength and the direction of that association.

That's pretty damned cool.

