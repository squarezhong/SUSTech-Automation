# Logic-Principles

- 由truth table得到逻辑表达式

1相加(SOP)，0相乘(POS)

### Boolean Algebra Theorems

![](img/class3/boolean_theorems_1.png)

![](img/class3/boolean_theorems_2.png)

![](img/class3/boolean_theorems_3.png)



- $X + \bar{X} Y = X + Y$

- Duality 对偶特性

The dual of a logic expression is obtained by swapping 0 and 1, and • and +. (variables do not change)

## K-map

binary sequence of  abc follows <font color='red'>**Gray code**</font>

![](img/class3/kmap_rule.png)

- Each implicant is a **product** term of the function

- implicants (蕴含项)

  - **Prime Implicants**: a group that covers the maximum possible number of adjacent squares.![](img/class3/kmap_prime_implicant.png)

  - **Essential Prime Implicants**: a prime implicant that ==covers a minterm== which is not covered by any other prime implicants![](img/class3/kmap_essential_prime_implicant.png)

### Minimized Logic Fucntions

#### K-map for Sums of Product

**All** essential prime implicants + other **needed** prime implicants

![SOP](img/class3/kmap_SOP.png)

![](img/class3/kmap_4variables.png)



#### K-map for Product of Sums

![](img/class3/kmap_POS.png)

#### K-map for XOR and XNOR

![2var](img/class3/kmap_xor_xnor_2.png)

![3var](img/class3/kmap_xor_xnor_3.png)

![4var](img/class3/kmap_xor_xnor_4.png)



#### Odd and Even Functions

- In general, for an n-variable Odd Function, the function is 1 if there are odd number of variables having logic 1

​	e.g. **XOR**

- For an n-variable Even Function, the function is 1 if there are even number of variables having logic 1

​	e.g. **XNOR**

#### DON'T-CARE Conditions

![](img/class3/kmap_not_care.png)

![](img/class3/kmap_not_care_eg.png)

#### 5-variable K-map

![](img/class3/kmap_5variables_1.png)

![](img/class3/kmap_5variables_2.png)

[Back to Outline](courses/EE202-17.md)



 
