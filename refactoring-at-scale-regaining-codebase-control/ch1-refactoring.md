# CH1 Refactoring

Refactoring is the process by which we restructure existing code (the factoring) without changing its external behavior.

Confidence in your ability to refactor allows you to lean toward action and start building a system sooner, well before you’ve developed a strong understanding of all the moving pieces, pitfalls, and edge cases.


## Benefits of refactoring

- Developer productivity
- Identifying Bugs

## Risk of Refactoring

- Serious regression, Refactoring untested code is very dangerous and highly discouraged.
- Unearthing Dormant Bugs, Just as refactoring can help you identify bugs, it can unintentionally unearth dormant
bugs.
- Scope Creep, Refactoring can be a little bit like eating brownies: the first few bites are delicious,
making it easy to get carried away and accidentally eat an entire dozen.
- Unnecessary Complexity

## When to Refactor

- Small Scope
- Code Complexity Actively Hinders Development
- Shift in Product Requirements
- Performance
- Using new technology

> Not all developers believe that performance improvements are a valid reason to refactor; some assert that a system’s performance is innately part of its behavior and therefore altering it in some way alters the behavior. I disagree. If we continue to define refactoring by using our generic system to which we provide a set of inputs, and continue to produce an expected set of outputs, then improving the speed (or memory burden) required to generate these outputs is a valid form of refactoring.

## When Not to Refactor

- For fun
- Because You Happened to Be Passing By
- To Making Code More Extendable
- When You Don’t Have Time


