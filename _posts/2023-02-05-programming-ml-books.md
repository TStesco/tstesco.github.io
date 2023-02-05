---
layout: post
title: Programming and Machine Learning Book Recommendations
date: 2023-02-05 12:00:00 -0000
image: bookshelf_rotated.jpg
tags: [software]
---

Several people recently asked me for resources that helped me while self-studying programming and machine learning so I compiled this list of books then decided to publish it below. I'm always looking for new book recommendations so shoot me an email or message on linkedin if you have one!

<div style="text-align: center;">
{% include captioned-image.html url="book_shelf_upright.jpg" description="Most of the programming and maths books on my bookshelf" style="height: auto; width: auto; max-height: 1200px;" %}
</div>

# The Craft of Programming

1. **Code: The Hidden Language of Computer Hardware and Software** ([goodreads link](https://www.goodreads.com/book/show/60091440-code)) \\
*by Charles Petzold* \\
The best easy-to-follow narrative explanation of how computers work from a bottom-up perspective. Circuits, transistors, adders, memory, logic gates, to assembler. the first several chapters may seem too cute, but that helps make the later material approachable to someone without any prior background in circuits.

1. **Programming: Principles and Practice Using C++** ([goodreads link](https://www.goodreads.com/book/show/2914066-programming))\\
*by Bjarne Stroustrup* \\
How to write programs in C++ that deal with ***memory allocation***, the horror! You may never need to write C/C++, but remember that Python is in essence an interface to run C/C++ code. Understanding common patterns can save you from ruin. [RAII](https://en.wikipedia.org/wiki/Resource_acquisition_is_initialization) to the rescue.

1. **The Pragmatic Programmer, 20th Anniversary Edition** ([goodreads link](https://www.goodreads.com/book/show/60633459-the-pragmatic-programmer-20th-anniversary-edition-your-journey-to-maste))\\
*by Andy Hunt, David Thomas* \\
Well-structured notes on reaching the zen state of mastery in programming for real applications.

1. **The Mythical Man-Month: Essays on Software Engineering** ([goodreads link](https://www.goodreads.com/book/show/13629.The_Mythical_Man_Month))\\
*by Frederick P. Brooks Jr.* \\
A classic on software project management. Why do software projects miss milestones and blow budgets? Why can't I double the programmers on the project to deliver it twice as fast? Unfortunately writing the program is only ~1/3 of the work and as programmers, we underestimate the equal parts efforts of testing and system integration.

1. **Code Complete 2 (Best Practices)** ([goodreads link](https://www.goodreads.com/book/show/4845.Code_Complete))\\
*by Steve McConnell* \\
What it says on the tin, encyclopedic content of programming best practices.


##### Currently reading

1. **The C Programming Language** ([goodreads link](https://www.goodreads.com/book/show/515601.The_C_Programming_Language))\\
*by Brian W. Kernighan, Dennis M. Ritchie* \\
The legendary book from the Bell Labs days of computing that brought the C language to the masses.


# Algorithms, Computer Science, and Optimization

1. **Introduction to Algorithms (3rd edition, aka CLRS)** ([goodreads link](https://www.goodreads.com/book/show/108986.Introduction_to_Algorithms))\\
*by Thomas H. Cormen, Charles E. Leiserson, Ronald L. Rivest, Clifford Stein* \\
The standard algorithms book simply referred to as CLRS, remains a surprisingly large component of undergrad CS at top-tier schools.

1. **Concrete Mathematics: A Foundation for Computer Science** ([goodreads link](https://www.goodreads.com/book/show/112243.Concrete_Mathematics))\\
*by Ronald L. Graham, Donald Ervin Knuth, Oren Patashnik* \\
A great introduction to mathematical thinking in the discrete world of computers. The genuine intrigue of the authors and plain language makes this book somewhat unique and perfect for self-study.

1. **Algorithm Design** ([goodreads link](https://www.goodreads.com/book/show/145055.Algorithm_Design)) \\
*by Jon Kleinberg, Éva Tardos* \\
Skip if you prefer CLRS, but may be a great alternative if you did not like it. Focuses more on designing and proving the correctness of algorithms.

##### Currently reading

1. **Structure and Interpretation of Computer Programs (2nd edition)** ([goodreads link](https://www.goodreads.com/book/show/43713.Structure_and_Interpretation_of_Computer_Programs)) \\
*by Harold Abelson, Gerald Jay Sussman, Julie Sussman*


1. **Discrete Mathematics and Its Applications (5th edition)** ([goodreads link](https://www.goodreads.com/book/show/1800803.Discrete_Mathematics_and_Its_Applications)) \\
*by Kenneth H. Rosen*

1. **Discrete and Combinatorial Mathematics (5th edition)** ([goodreads link](https://www.goodreads.com/book/show/1575542.Discrete_and_Combinatorial_Mathematics)) \\
*by Ralph P. Grimaldi*

Honourary mentions to [The Art of Computer Programming](https://www-cs-staff.stanford.edu/~knuth/taocp.html) series by Donald E. Knuth, which I have heard is a classic worth consideration.


# Distributed Systems

1. **Designing Data-Intensive Applications (aka DDIA)** ([goodreads link](https://www.goodreads.com/book/show/23463279-designing-data-intensive-applications))\\
*by Martin Kleppmann* \\
The most comprehensive and detailed book on how modern distributed systems work and how their components are implemented. How do databases work? How acan distributed databases be reliable under (most) fault conditions? How can I deal with CAP theorem? What are the tradeoffs of batch vs. stream processing?

1. **System Design Interview – An Insider's Guide: Volume 2** ([goodreads link](https://www.goodreads.com/book/show/60631342-system-design-interview-an-insider-s-guide))\\
*by Alex Xu, Sahn Lam* \\
Great walkthroughs on how to design scalable distributed systems in an interview whiteboarding context.

# Machine Learning and Artificial Intelligence

1. **Pattern Recognition and Machine Learning** ([goodreads link](https://www.goodreads.com/book/show/55881.Pattern_Recognition_and_Machine_Learning?ac=1&from_search=true&qid=xafeIOEA8y&rank=2))\\
*by Christopher M. Bishop* \\
Perhaps the most standard book on Bayesian machine learning. A great source and reference for: linear models, Support Vector Machines (SVMs), Bayesian network (AKA probabilistic graphical) models, Markov Chain Monte Carlo (MCMC), Principal Component Analysis (PCA), Hidden Markov Models (HMMs). There is little discussion of the dark alchemy of feature engineering and representation learning.

##### Currently reading

1. **Deep Learning (Adaptive Computation and Machine Learning)** ([goodreads link](https://www.goodreads.com/book/show/24072897-deep-learning))\\
*by Ian Goodfellow, Yoshua Bengio, Aaron Courville* \\
Focuses on solving the representation learning problem by decomposing it into a ***deep*** hierarchy of sub-representations that can each be ***learned*** . While this book pre-dates [Attention Is All You Need](https://arxiv.org/abs/1706.03762) and the rise of transformer network architectures it does provide a rigorous foundation for deep learning including modern methods.

1. **Deep Learning with Python** ([goodreads link](https://www.goodreads.com/book/show/33986067-deep-learning-with-python))\\
*by François Chollet*

1. **Linear Algebra Done Right (3rd edition)** ([goodreads link](https://www.goodreads.com/book/show/24848812-linear-algebra-done-right))\\
*by Sheldon Axler*