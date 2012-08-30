% Applied Linear Algebra
% Jason Grout
% Fall 2012

<frontmatter>

Preface
=======

The chapter titles in these notes correspond with the chapter titles
in the book
[*Numerical Linear Algebra*](http://people.maths.ox.ac.uk/trefethen/text.html)
by Trefethen and Bau, published by SIAM.  The sections below are
labeled "Lectures" because the chapters in the book are labeled
"Lectures", but they may not correspond with single class periods.

<div class="html">A nicely typeset version of these notes is
[here](http://sage.math.washington.edu/home/jason/applied-linear-algebra.pdf).</div>

An online version of these notes is available that includes some
enhancements from [Sage](http://www.sagemath.org).

**Make sure to read and understand each chapter as we cover it in class.**

Class Plans
===========

27 Aug 2012
-----------

#. Some highlights of why studying applied, numerical linear algebra
 is important.

    - Calculating a determinant is both impossibly hard and
      numerically bad when using cofactor expansion.  Instead, use LU
      decomposition or similar
    - Calculating eigenvalues using the characteristic polynomial is
      bad, since it involves both a determinant and polynomial
      root-finding (numerically unstable).  See
      [Wilkinson's polynomial](http://en.wikipedia.org/wiki/Wilkinson's_polynomial).

    <sagecell>

    ```
    wilkinson = prod((x-i) for i in [1..20]).polynomial(QQ)
    x=wilkinson.variables()[0]
    eps=2^-31
    c=-210
    @interact
    def _(precision=slider(40,100,1,default=53), coefficient=slider([c-eps..c-eps/20,step=float(eps/20)]+[c..c+eps,step=float(eps/20)],default=c)):
        R = ComplexField(precision)
        perturbed = wilkinson.change_ring(R)+(R(coefficient)-c)*x^19
        original_roots = [1..20]
        perturbed_roots = [i[0] for i in perturbed.roots()]
        # match up roots
        rootlist=[]
        for r in [1..20]:
            # find the closest root left
            matching_root = min([[i, abs(r-i),index] for index,i in enumerate(perturbed_roots)], key=lambda x: x[1])
            rootlist.append([r, matching_root[0], matching_root[1]])
            perturbed_roots.pop(matching_root[2])
  
        html("Changing the $x^{19}$ term from $-210x^{19}$ to $%sx^{19}$ gives the following differences in roots"%R(coefficient))
  
        html.table(rootlist, header=["Original root", "Perturbed root", "Distance"])
```

      </sagecell>

#. Review of key concepts from linear algebra (see exercises).


29 Aug 2012
-----------

#. Present the rest of Exercise 1.1--1.3

#. Discuss the connection between matrices and linear transformations,
   including invertible matrices.

#. Discuss coordinates briefly.

05 Sep 2012
-----------

#. Present the rest of the exercises for Lecture 1

#. Complex numbers

#. Start working on exercises for Lecture 2.

</frontmatter>

<mainmatter>