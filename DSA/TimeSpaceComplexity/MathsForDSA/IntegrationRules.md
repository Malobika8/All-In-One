# Integration Rules
The integral rules are used to perform the integral easily. In fact, the integral of a function f(x) is a function F(x) such that 
d/dx (F(x)) = f(x). 

For example, d/dx (x2) = 2x and so ∫ 2x dx = x2 + C. i.e., the integration is the reverse process of differentiation. But it is not possible 
(not easy) every time to apply the reverse process of differentiation to evaluate the integrals. The integration rules would help a lot in 
this regard.

Let us see what are the integration rules of different functions along with examples.

## What are Integration Rules?
The integration rules are rules used to integrate different types of functions. 

We have seen that ∫ 2x dx = x2 + C as d/dx (x2) = 2x. 

This can be obtained by the power rule of integration that says ∫xn dx = xn+1/(n+1) + C, where 'C' is the integration constant (which we add 
after the integral of any function). Using this rule, ∫ 2x dx = 2 [x1+1/(1+1) ]+ C = 2 (x2/2) + C = x2 + C and we got the same answer.
Now, you might have understood the importance of integration rules. There are different types of integral rules and the most commonly used 
ones are mentioned below:

![integration-rules-1647501163](https://github.com/Malobika8/All-In-One/assets/111234135/01df61ad-1fbd-45bf-9817-e6bff1bc5428)

## Basic Integration Rules
Here are the basic integration rules where each of them can be cross verified by differentiating the result. 

- Power rule of integration is, ∫ xn dx = xn+1/(n+1) + C
- Integral of 1 is, ∫ 1 dx = x + C.
- Integral of ex is, ∫ ex dx = ex + C
- Integral of ax is, ∫ ax dx = ax / ln a + C
- Integral of 1/x is, ∫ 1/x dx = ln |x| + C
- 
Apart from these, we use the following properties of integrals when sum/difference of terms is present in the place of integrand.

- ∫ [f(x)+g(x)] dx = ∫ f(x) dx + ∫ g(x) dx
- ∫ [f(x)-g(x)] dx = ∫ f(x) dx - ∫ g(x) dx
- ∫ a f(x) dx = ∫ f(x) dx + C, where 'a' is a constant


## Integration Rules of Trigonometric Functions
There are 6 trigonometric functions: sin, cos, tan, csc, sec, and cot. Here are the integration rules of all these trigonometric functions:

- Integral of sin x is, ∫ sin x dx = -cos x + C.
- Integral of cos x is, ∫ cos x dx = sin x + C.
- Integral of tan x is, ∫ tan x = ln (sec x) + C (or) -ln |(cos x)+C
- Integral of csc x is, ∫ cosec x dx = ln |cosec x - cot x| + C (or) - ln |cosec x + cot x| + C (or) ln | tan (x/2) | + C
- Integral of sec x is, ∫ sec x dx = ln |sec x + tan x| + C (or) (1/2) ln | (1 + sin x) / (1 - sin x) (or) ln | tan [ (x/2) + (π/4) ] | + C
- Integral of cot x is, ∫ cot x dx = ln |sin x| + C
  
Apart from these, there are some other rules that involve a combination of trigonometric functions.

- ∫ sec2x dx = tan x + C
- ∫ cosec2x dx = -cot x + C
- ∫ sec x.tan x dx = sec x + C
- ∫ cosec x . cot x dx = -cosec x + C

## Integration Rules of Inverse Trigonometric Functions
There are 6 inverse trigonometric functions: arcsin (sin-1), arccos (cos-1), arctan (tan-1), arccsc (csc-1), arcsec (sec-1), and arccot (cot-1). 

Here are the integration rules of these inverse trigonometric functions.

- ∫ sin-1x dx = x sin-1x + √(1 - x2) + C
- ∫ cos-1x dx = x cos-1x - √(1 - x²) + C
- ∫ tan-1x dx = x tan-1x - ½ ln |1+x2| + C
- ∫ csc-1x dx = x csc-1x + ln |x + √(x2 - 1)| + C
- ∫ sec-1x dx = x sec-1x - ln |x + √(x2 - 1)| + C
- ∫ cot-1x dx = x cot-1x + ½ ln |1+x2| + C
  
We actually do not need to remember these rules, instead, we can apply the integration by parts rule to derive each of these quickly.

Besides these, we have several other integration rules that involve the inverse trigonometric functions:

- ∫1/√(1 - x2).dx = sin-1x + C
- ∫ 1/(1 - x2).dx = -cos-1x + C
- ∫ 1/x√(x2 - 1).dx = sec-1x + C
- ∫ 1/x√(x2 - 1).dx = -cosec-1 x + C
- ∫1/(1 + x2).dx = tan-1x + C
- ∫ 1/(1 +x2 ).dx = -cot-1x + C
  
These rules are directly derived from the derivatives of inverse trig functions.


## Integration Rules of Special Functions

Other than the rules that we have seen in the previous sections, we have some integration rules that are used to integrate some special 
type of rational functions where the denominator involves squares. 

They are as follows:

- ∫1/ (x2 - a2) dx = (1/2a) log|(x-a)/(x+a)| +C
- ∫1/ (a2 - x2) dx = (1/2a) log|(a+x)/(a-x)| +C
- ∫ 1/ √(x2 + a2) dx = log |x + √(x2 + a2)|+C
- ∫1/ √(x2 - a2) dx = log |x + √(x2 - a2)|+C
- ∫1/ (a2 + x2) dx = (1/a) tan -1 (x/a) + C
- ∫ 1/ √(a2 - x2) dx = sin-1 (x/a) +C
  
There are some other integration rules that involve square roots in integrands.

- ∫√(a2 - x2).dx = x/2 · √(a2 - x2) + a2/2· sin-1 x/a + C
- ∫√(x2 + a2).dx = x/2 · √(x2 + a2) + a2/2· log |x + √(x2 + a2)| + C
- ∫√(x2 - a2).dx = x/2 · √(x2 - a2) - a2/2· log |x + √(x2 - a2)| + C
  
These 3 rules can be obtained by using the substitution method of integration.


## ILATE Rule of Integration
The ILATE rule of integration is used in the process of integration by parts. This is applied to integrate the product of any two different 
types of functions. 

The integration by parts rule says:

#### ∫ u dv = uv - ∫ v du

But when we have a product of functions u × dv, we get confused what function should be u and what function should be dv. 

In this case, we use ILATE rule where:

- I : Inverse trigonometric functions
- L: Logarithmic functions
- A: Algebraic functions
- T: Trigonometric functions
- E: Exponential functions
  
The first function "u" should be chosen with respect to the above order of functions given the first priority to the function that appears 
first in the above list. This rule can be sometimes referred to as LIATE as well. This rule is used to integrate the inverse trigonometric 
functions (as mentioned in one of the previous sections) and the logarithmic functions. One of the most important applications of this rule 
of integration is integral of ln x, which is, ∫ ln x dx = x ln x - x + C. 

We can derive this rule as follows:

∫ ln x dx = ∫ ln x · 1 dx

Here, ln x is a log function and 1 is an algebraic function. So using the order of ILATE, ln x should be the first function u. i.e.,

let u = ln x and dv = 1. Then

du = (1/x) dx and v = ∫ 1 dx = x.

By the integration by parts rule,

∫ u dv = uv - ∫ v du

∫ ln x · 1 dx = (ln x) (x) - ∫ x (1/x) dx

∫ ln x dx = x ln x - ∫ 1 dx = x ln x - x + C.

Thus, whenever there is no direct rule to integrate a function and there is only one function to integrate, assume the second function as 1 
and apply the integration by parts rule.

## Rules of Substitution Method of Integration
When none of the above integration rules can be applied, and if some part of the integrand is the derivative of the other part of the 
integral, then we use the substitution method. 

In this method:

Assume a part of the integrand to be u.

Find du.

Convert the given integral completely in terms of u. Then integrate using one of the above-mentioned rules.
Substitute the value of u back in the result.

Example: Find the integral of ∫ 2x sin x2 dx.

Solution:

Let x2 = dx. Then 2x dx = du.

∫ 2x sin x2 dx = ∫ sin u du

= - cos u + C

= - cos x2 + C

Using this substitution method, we can derive a few other integration rules as follows:

- ∫ f '(x) / f(x) dx = ln |f(x)| + C
- ∫ f '(x) / √(f(x)) dx = 2√[f(x)] + C
- ∫ sin ax dx = (1/a) (- cos ax) + C ;
- ∫ cos ax dx = (1/a) (sin ax) + C;
- ∫ 1/(ax + b) dx = (1/a) ln |ax + b|, etc. (similar rules can be derived for other functions as well)
  
## Rules of Integration Using Partial Fractions
To integrate a rational function, we first split it into partial fractions using one of the following rules and then apply the rule 

∫ 1/(ax + b) dx = (1/a) ln |ax + b| + C 

to integrate each partial fraction.

![i](https://github.com/Malobika8/All-In-One/assets/111234135/1d4ea6d7-626c-4ea0-a3b0-769681e4d491)


## Integration Rules of FTC
FTC (Fundamental Theorem of Calculus) provides two rules that are helpful in integration. The first rule is used to find the derivative of 
indefinite integrals whereas the second rule is used to evaluate the definite integrals.

FTC 1: d/dx ∫ax f(t) dt = f(x)

FTC 2: ∫ab f(t) dt = F(b) - F(a), where F(x) = ∫ab f(x) dx

Example: Find d/dx ∫2x sin t2 dt.

Solution:

Here, f(t) = sin t2 and a = 2. By the first fundamental theorem of calculus, we have:

d/dx ∫ax f(t) dt = f(x)

d/dx ∫2x sin t2 dt = f(x) = sin x2.

## Important Notes on Integration Rules:

- The integration constant (C) must be added for every result of an indefinite integral.
- The integration constant doesn't appear in the result of a definite integral.
- Apply the LIATE rule to integrate a product of two different types of functions.
- To integrate the quotient of functions, the substitution method is useful in most cases.


## Integration Rules Examples

### Example 1: Evaluate the integral ∫ (x4 + 3x2 + x) / x2 dx.

##### Solution:

Let us decompose the given fraction.

∫ (x4 + 3x2 + x) / x2 dx = ∫ x4 / x2 dx + ∫ 3x2 / x2 dx + ∫ x/ x2 dx

= ∫ x2 dx + 3 ∫ 1 dx + ∫ (1/x) dx

= (x3/3) + 3x + ln |x| + C (using the integration rules)

*Answer: (x3/3) + 3x + ln |x| + C*

### Example 2: Find the value of the integral ∫ x sin x dx.

#### Solution:

The integrand has a product. So we will integrate using the integration by parts. Using ILATE rule,

let u = x and dv = sin x dx. Then

du = 1 dx and v = -cos x.

Now, we will substitute these values in the rule below and apply the integration rules.

∫ u dv = uv - ∫ v du

∫ x sin x dx = x (-cos x) - ∫ (-cos x) dx

= - x cos x + ∫ cos x dx

= - x cos x + sin x + C

*Answer: - x cos x + sin x + C.*

### Example 3: What is the value of ∫ (x3) / (x4 - 1) dx?

#### Solution:

We will solve this using the substitution method of integral calculus.

Let x4 - 1 = u. Then 4x3 dx = du and from this, x3 dx = (1/4) du.

Then the given integral becomes:

∫ (1/4) du 1/u = (1/4) ∫ 1/u du

= (1/4) ln |u| + C

Substitute u = x4 - 1 back here,

= (1/4) ln |x4 - 1| + C

*Answer: (1/4) ln |x4 - 1| + C.*
