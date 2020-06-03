---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "An Analysis of a Jensen's Inequality Problem"
subtitle: ""
summary: ""
authors: [Patrick Ma]
tags: [Machine Learning]
categories: []
date: 2020-05-24T15:34:09-04:00
lastmod: 2020-05-24T15:34:09-04:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

## Question

Give a non-negative random variable $X$, and positive integers $n$, $m$, show that if $n \le m $, $[E(X^{n})]^{\frac{1}{n}} \le [E(X^{m})]^{\frac{1}{m}}$.

### Analysis: 

Intuitively, the problem may need techniques like Jensen's Inequality as there is expectation and concave ($a^{\frac{1}{m}}$) & convex functions ($a^{m}$). However, it would be hard to use Jensen directly without proper transformation. Recall that Jensen's Ineuqality states:
$$
f(EX) \le Ef(X) ~~~~~~~~~ \text{if  $f(.)$ is convex} \\
$$

$$
f(EX) \ge Ef(X) ~~~~~~~~~ \text{if  $f(.)$ is concave.}
$$



#### Attempt 1

We can try to apply Jensen partially to the LHS to see if it gives us a intermediate expression.

We know that $f(a)=a^n$ is convex on $[0,\infty)$ if $n \ge 1$.  Using Jensen, we have 
$$
E(X^n) \ge (EX)^n \\   [E(X^n)]^{\frac{1}{n}} \ge [(EX)^n]^{\frac{1}{n}}=EX
$$
This is not we want as Jensen finds a lower bound for the LHS and proving $EX \le [E(X^{m})]^{\frac{1}{m}}$ does not lead to our goal.

#### Attempt 2

What about applying to the concave function  ($a^{\frac{1}{m}}$) ?

We know that $f(a)=a^{\frac{1}{n}}$ is concave on $[0,\infty)$ if $n \ge 1$.  Using Jensen, we have 
$$
[E(X^n)]^{\frac{1}{n}} \ge E(X)^{n\frac{1}{n}}=EX
$$
Same lower bound. Not helpful, either!

#### Attempt 3

The failure in finding a good intermediate form motivates me to look back and  exam the correctness of the proposition in a basic case.

Recall that variance of a randome variable is always non-negative:
$$
Var(X) = E(X-EX)^2		=EX^2-2E(XEX)+(EX)^2
$$

$$
= EX^2-(EX)^2		\ge 0.
$$



We have:
$$
(EX)^2 \le EX^2 	\\\Leftrightarrow EX \le (EX^2)^{\frac{1}{2}} 	\\\Leftrightarrow (EX^1)^{\frac{1}{1}} \le (EX^2)^{\frac{1}{2}},
$$
which is true for non-negative random variable.

In this case, $n=1, ~ m = 2$. Can we try to reverse the general case into a well-formatted form like $(EX)^2 \le EX^2$?
$$
(EX^n)^{\frac{1}{n}} \le (EX^m)^{\frac{1}{m}}  \\
\Leftrightarrow (EX^n)^{\frac{m}{n}} \le EX^m \\
\Leftrightarrow (EX^n)^{\frac{m}{n}} \le EX^{n\frac{m}{n}}
$$
Boom! The reversed roadmap for transforming basic case into our goal worked! Here we have a random variable $Y=X^n$, convex function $g(a)=a^{\frac{m}{n}}$ as $\frac{m}{n} \ge 1$. The final form can be treated as $g(EY) \le E[g(Y)]$, which is true by Jensen's Inequality! We can finally prove the proposition!



### Proof

Let $Y=X^n, g(a) = a^{\frac{m}{n}}$.

Since
$$
g''(a) = \frac{m}{n}.(\frac{m}{n}-1).a^{\frac{m}{n}-2} \ge 0 ~~\forall a \in [0, \infty),
$$
$g(a)$ is convex on $[0,\infty)$.

By Jensen's Inequality:
$$
(EX^n)^{\frac{m}{n}} = (EY)^{\frac{m}{n}} \le E(Y^{\frac{m}{n}}) =  E([X^n]^{\frac{m}{n}})=EX^m
$$

$$
\Leftrightarrow [E(X^{n})]^{\frac{1}{n}} \le [E(X^{m})]^{\frac{1}{m}}. ~~~~~~~~~~~\square
$$



### Conclusion

We solved the problem by tracing back to the basic case and used it as a guide for proving the general case. Sometimes mathematical gymnastics helps us a lot.

