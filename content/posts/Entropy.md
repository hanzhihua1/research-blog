---
title: Entropy in Physics and Machine Learning
date: "2020-02-02T22:40:32.169Z"
template: "post"
draft: false
slug: "entropy"
category: "Information Geometry"
tags:
  - "Information Geometry"
description: "Information Geometry Part 0"
socialImage: "/media/image-3.jpg"
---

# 0. Entropy in physics and machine learning

The goal of information theory is to achieve one thing: to quantify the amount of information contained in a random variable.

## Random variables

What is a variable? A variable is simply a number in a box. $x = 5$ means that inside the box $x$, we have the number 5.

**A random variable is a variable that has it's value drawn according to some probability distribution.**

Unlike variables, you can't just open the what the box is because you don't know what's inside. It's _random_.

That is, imagine a computer drawing a random number from a probability distribution and assigning it to $x$. The variable $X$ is then assigned some number $x$. The chance that $X = x$ is given by some probability $p(x)$, or $p(X = x)$. So really, specifying a distribution defines a random variable, and vice versa.

Again. We can never know what $X$ is. We can always know the probability of $X = x$, but the closest thing we can write is that

$$
X \sim p(x | \theta)
$$

If we know $X$ is from some family of distributions, then knowing the all the parameters $\theta$ also tells us what $X$ is.

In the notes, we will use random variables and probability distribution interchangably.

## The definition of entropy

The shannon entropy can be thought of as the uncertainty of a random variable. In these notes we will always take the logarithm to be base 2. It is defined by:

$$
\boxed{H(X)=-\sum_{x \in \mathcal{X}} p(x) \log p(x)}
$$

In physics, this is known as the Gibbs entropy. If we pick $p(x) = 1/n$, we obtain:

$$
H(X)=-\sum_{x \in \mathcal{X}} \frac{1}{n} \log \frac{1}{n} = \log(n)
$$

which is the number of microstates, or Boltzmann's formula.

Entropy can be thought of as the minimum number of binary questions to determine the value of $X$. Thus, entropy has units of **bits**.

We can write entropy as an expected value:

$$
H(X)=E_{p}[\log \frac{1}{p(x)}]
$$

## Information content

We see that in the definition of entropy we have the quantity

$$
I(X) = \log\left(\frac{1}{p(x)}\right)
$$

which is usually referred to as information content. Information content roughly measures the suprisal of seeing some value $X = x$, since we are more suprised the smaller $p(x)$ is. The log is there to make sure entropy has some nice properties. (additivity, non-negativity)

## Joint and Conditional entropy

The joint entropy is for two random variables, and is defined as

$$
H(X, Y)=-\sum_{x \in \mathcal{X}} \sum_{y \in \mathcal{Y}} p(x, y) \log p(x, y)
$$

as an expected value:

$$
H(X, Y)=-E_{p(x,y)} \log p(X, Y)
$$

The conditional entropy is defined as

$$
\begin{aligned}
H(Y | X) &=\sum_{x \in \mathscr{X}} p(x) H(Y | X=x) \\
&=-\sum_{x \in \mathscr{X}} p(x) \sum_{y \in \mathscr{Y}} p(y | x) \log p(y | x) \\
&=-\sum_{x \in \mathscr{X}} \sum_{y \in \mathscr{Y}} p(x, y) \log p(y | x) \\
&=-E_{p(x, y)} \log p(Y | X)
\end{aligned}
$$

Chain rule:

$$
H(X, Y)=H(X)+H(Y | X)
$$

In general, entropy acts like a measure on the sample space where random variables live. Here is a quick diagram.
![](https://upload.wikimedia.org/wikipedia/commons/thumb/d/d4/Entropy-mutual-information-relative-entropy-relation-diagram.svg/2560px-Entropy-mutual-information-relative-entropy-relation-diagram.svg.png)

## Relative Entropy

Let $X$ be a random variable with distribution $p(x)$. Suppose that we wished to approximate $X$ with another distribution $q(x)$. How many bits of information might we lose?

To answer this question, we can define two related quantities. First, since we are replacing $p(x)$ with $q(x)$, we should replace the information content of $p(x)$ with $q(x)$ and take its expected value.

Thus, the cross entropy is defined by:

$$
H_q(p) = H(X) = \sum_x p(x) \log(q(x))
$$

which for clarity, has the notation $H_q(p)$. Now, we only need to take the expected true information content and subtract the two:

$$
D(p || q) = H_q(p) - H(p)
$$

$$
D(p || q) = \sum_x p(x) [\log(q(x) - \log(p(x))]
$$

which known as the KL divergence. I like to read this as entropy difference $D(p || q)$ of replacing $p$ by $q$.

$$
D(p || q) = -\sum_x p(x) \log\left(\frac{q(x|\theta)}{p(x|\theta)}\right)
$$

Note that the variable $x$ is essentially a dummy variable. In fact, for all definitions of entropy, it doesn't depend on $x$, but rather the random variable $X$ or distribution $p(x|\theta)$.

## Information = Entropy?

What is the relation between information and entropy? Why do we care?

The reason has to do with [https://en.wikipedia.org/wiki/Landauer%27s_principle](https://en.wikipedia.org/wiki/Landauer%27s_principle).

[Szilard's_engine](https://en.wikipedia.org/wiki/Entropy_in_thermodynamics_and_information_theory#Szilard's_engine)

You can prove using Szilard's engine that, a Maxwell's demon would not violate the Second Law of Thermodynamics since, for the demon to lift the gates, he must increase the entropy in his brain. Erasing the information in his brain, would cause the entropy of the environment to increase.

So physically, information = entropy!

[https://www.youtube.com/watch?v=8Uilw9t-syQ](https://www.youtube.com/watch?v=8Uilw9t-syQ)
