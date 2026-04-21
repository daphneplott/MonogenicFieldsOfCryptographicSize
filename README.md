# Monogenic Fields Of Cryptographic Size
This repository contains code related to the paper Monogenic Fields of Cryptographic Size by Swechchha Adhikari, Max Brown, Stephen McKean, Daphne Plott, and Parker Torgersen.

This code contains test and exploratory computations regarding the polynomial transform F(x) = x^n f(1/x + c + x) where n is the degree of f(x). The code contains documentation and commentary upon results where applicable. Along with test computations it contains some personal brainstorming notes. These will be labeled where they show up. The code is all designed to run through Sage.

Much of these codeblocks were written before our naming convention of F(x) as the transformed polynomial was solidified. As such, there are many places where g(x) refers to the transformed polynomial instead of F(x). 

I use the term "squareful" in my notes as a shorthand for "not squarefree". This may or may not be the correct technical term.

This code is split into four main categories regarding different properties of the transformation. Here is a list of what is included in the repository:

## Irreducibility 

### Irreducibility_CombinationsOfx^n.ipynb

This file generates examples of single-transformed polynomial, and will check the irreducibility of the resulting transformation. It is currently set to look at degree 6 polynomials, but this can be updated easily.

### Irreducibility_CompareCWithReverse.ipynb

This file will take some f(x) with some c value, and calculate the g(x) - which may more clearly be called f'(x) - such that applying the transformation with c = 0 to g(x) will result in the same F(x). It does this to compare the irreducibility of f(x) and the irreducibility of g(x). Preliminary data implies that f(x) is irreducible if and only if g(x) is, and this is supported by the findings of our paper. 

This file also includes some details about how to apply the reverse transformation in a computational setting. For more information on this, we refer the reader to Cafure and Cesaretto's paper "Irreducibility Criteria for Reciprocal Polynomials and Applications" found on JSTOR at [https://www.jstor.org/stable/10.4169/amer.math.monthly.124.1.37?seq=7]. The computational setup, which includes matrix multiplication, is much the same. However, the matrix used to multiply against the coefficients of F(x) is different. This matrix needs to be updated with the h_k(x) polynomials that correspond to the specific c value you are using. The matrix included in Cafure and Cesaretto's paper is esentially for the sequence of h_k(x) polynomials that correspond to c = 0.

### Irreducibility_CriteriaWithC=_2.ipynb

This file tests a very specific criteria found at [https://mathscinet.ams.org/mathscinet/article?mr=3187737]. It provides irreducibility criteria for a very specific subset of our transformation. This subset later contradicted with our attempts to look at monogenicity. It was an early investigation that proved less necessary with our broader irreducibility criteria, and as such is not included in our published paper.

### Irreducibility_FactoringFailedTransforms.ipynb

Thie file factors transformations where f(x) was irreducible, but F(x) was not. It factors from a list of 'failed' transformation included in the file. It additionally factors F(1) and F(-1).

### Irreducibility_FactoringFromFileWithPredictionMath.ipynb

This file factors transformations from a given file, using details about the coefficients of f(x). 

It also includes a piece of math used to predict 'failed' transformations where f(x) is irreducible but F(x) is not. This math is not included in the published paper as it is inefficient, and an early attempt to describe irreducibility.

### Irreducibility_TimeCompareDifferentSolutions.ipynb

This file runs an empirical time comparison of the sage math factoring algorithm against an algebraic analysis of the coefficients of F(x) in terms of the coefficients of f(x). It was determined this solution was not time effective. This was an early investigation into a possible irreducibility criteria that did not work out.

### Irreducibility_FialedTransformData.txt

This data file contains the coefficients of degree 4 polynomials and c values for which f(x) is irreducible but F(x) is not. The data in this file is formatted as ",l,m,n,o,c" to be used as f_x = x^4 + l\*x^3 + m\*x^2 + n*x + o with c being the transform value c.

## Monogenicity

### Monogenicity_BackTransformWithPalindromic.ipynb

This file tries to answer the following question: Given the result of some transformation, can we find a c value such that the reverse transformation of F(x) with regard to this c value will give us a palindromic polynomial f(x)? This was an attempt to prove that the set of transformed polynomials, or the set of the resulting polynomials after multiple transformations, was the same as the general set of palindromic polynomials. This was the start of a potential approach to showing there are an infinite number of monogenic transformed polynomials. Most (if not all) of the code in this file was generated by ChatGPT. The results of this test were that not every palindromic polynomial can be reversed to some palindromic polynomial.

### Monogenicity_Investigations.ipynb

This file investigates monogenicity by calculating the differences between roots of F(x), which are part of the discriminant of F(x). It yeilded no useful information as we were able to figure out.

### Mongenicity_SimpleCheck.ipynb

This file takes a given c and f(x) value, creates F(x), and calculates the discriminants of both functions and the number fields they generate.

### Monogenicity_AlgebraicChecksonTheorem.ipynb

This file runs checks on the expression for the discriminant we propose in our paper againsts the discriminant calculated by sage. It also will iteratively apply the transform and track properties of F(1) and F(-1). It contains some personal notes about the application of a different theorem to determine the discriminant based on functional composition found in this paper: https://faculty.bard.edu/cullinan/disccomp.pdf. While this particular application fell through based on some holes, a separate computation found the same expression, and that is what is included in our paper.

### Monogenicity_BacksolvingForg(1).ipynb

This file has some functionality to try and backsolve for F(1), according to calcuations worked out by hand. This did not help square-free factoring because there are added terms in the expression I found. 

It then compares the size of F(1) between a polynomial starting at degree 1, and a polynomial starting at degree 8, both getting up to a final polynomial of degree 1024. The sizes were much the same, and not helpful for squarefree calculations.

It contains a lot of notes to self about how to determine if F(1) and F(-1) are squarefree, some of which are interesting questions, although mostly from a number theory perspective. 

It lastly looks at how the addition of squarefree/squareful numbers are squarefree or squareful. No useful pattern was observed.

### Monogenicity_DiscriminantsInTermsOfa.ipynb

This file looks at the discriminant of multiple iterations of applying the transform to f(x) = x - a. It calculates the discriminants in terms of a generic a and c value.

### Monogenicity_IterateThroughTransform.ipynb

This file has code that will loop through different degree 2 polynomials, and iteratively apply the transformation. It tracks when and how often we expect a transformed polynomial to be monogenic. 

This file has code that will loop through different degree 3 polynomials, and compare when f(x) is/isn't monogenic against when F(x) is/isn't monogenic.

This file also contains some notes to self about proving that F(x) isn't monogenic if f(x) isn't monogenic, which is proven in our paper.

### Monogenicity_ReverseTransform.ipynb

This file contains code to apply the reverse transformation to different sizes of F(x). 

It also contains thoughts about trying to reverse any palindromic polynomial into another palindromic polynomial. Refer back to Monogenicty_BackTransformWithPalindromic.ipynb for more notes on this.

It contains some rambling thoughts about trying to prove an infinite number of these stacks will be monogenic.

### Mongenicity_SquareFreeAlgorithms.ipynb

This file contained an idea for an algorithm to check if a number was squarefree. This algorithm is not time efficient, and doesn't improve upon current methods built into Sage.

### Monogenicity_g(1)vs(g_1).ipynb

This file tries to analyze F(1) and F(-1) for when they may be squarefree. It contains code that looks at the parity of the different coefficients of F(x) and code that will iterate through the transformation and print out the factored values of F(1) and F(-1). It contains code that tracks certain interesting properties over many starting polynomials and iterations, tracking how often it is squarefree, how often the gcd is one, how often iterations will repeat factors of F(1) or F(-1), and how often those values are zero. 

It also contains code that considers how f(c+2) being squarefree as a polynomial (nonzero discriminant) may related to how F(1) is squarefree as an integer. The data gathered here suggested that f(c+2) could have a nonzero discriminant, but F(1) could still be squareful. However, if f(c+2) has a discriminant of zero, then F(1) must be squareful.

## Galois Groups

### GaloisGroups_GaloisGroupsWithDictionary.ipynb

This file will keep track of the Galois Groups of degree-5 f(x) and F(x), as well as if they produce monogenic number fields, save this in a dictionary, and then writing that to a file.

### GaloisGroups_GaloisGroupData.txt

This keeps track of the data collected according to the previous file. At the beginning of a section, it will describe what type of f(x) we used, and the ranges of the coefficients and different c values used. It then lists the counts for different Galois Group combinations. The data is ordered as f(x) Galois Group, F(x) Galois Group (listed as None if they were reducible), if f(x) produced a monogenic number field, and if F(x) produced a monogenic number field. To the side I have noted the order of the groups (which may contain some errors), and comments where I believed that F(x) had an abelian Galois Group. This was mostly determined by if F(x) didn't have any semi-direct products, or anything that was specifically non-Abelian (this may also contain some errors, I don't have a lot of experience with Galois theory).

## Normal Extensions

### Normal_NormalExtensions.ipynb

This file will loop through different polynomials, or generate random polynomials, and count how often f(x) is/isn't Normal, and how often F(x) is/isn't Normal. It also has functionality to print out various examples. It has a code block that lists a few examples where f(x) is not Normal but F(x) is, and computes the Galois Groups.

The general findings associated with this is that f(x) doesn't have to be Normal for F(x) to be Normal, and f(x) being Normal doesn't imply that F(x) must be. There are very few instances found where F(x) was Normal, especially when f(x) was Normal as well.

### Normal_NormalTransforms.ipynb

This file takes a few examples of transforms, and looks at the term (a-c)^2 - 4 for each a being a root of f(x). This comes from the expression for a root of F(x) in terms of the roots of f(x). In theory, if each of these terms are perfect squares under the Number Field created by F(x), then F(x) should be Normal.

### Normal_ExampleTransforms.ipynb

This file takes a few examples of transforms, and tries to look at the monogenicity of F(x), and tries to look at the expression of each root in terms of the main root of the Number Field. When I wrote these tests, it was under the assumption that the examples had both f(x) and F(x) Normal, but in fact it had f(x) Normal, but F(x) reducible, which may skew any results. These examples are not included in Normal_Data.txt.

### Normal_Data.txt

This lists example instances from Normal_NormalExtensions.ipynb. Each instance is separated by a line of dashes. The first piece of data is an indication like "True, False" or "Normal". If they are two booleans, the first indicates if f(x) is Normal, and the second indicates if F(x) is Normal. The word "Normal" indicates a "True, True" instance. Then, f(x) and c are listed. They are on the same line, and only have a space in the middle. For example, "x^4 - 8* x^2 - 8* x - 2 -2" indicates f(x) = x^4 - 8* x^2 - 8* x - 2, and c = -2. Sometimes F(x) is listed below that. In some instances, the Galois Groups of f(x) then F(x) are listed. These are not always listed due to time computing restraints in the data collection.
