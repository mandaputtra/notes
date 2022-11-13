# CH 8 Strategies for execution

## Team Building

Pair Programming, could help a lot ~ especially with the SME.

## Keeping Everyone Motivated

Refactoring could be a boring project. We should gradually motivate team and individuals. Create task that are meaningfull to them to refactor.

- Measure your team/individual goals

## Unearthed Bugs

> There are a number of factors to consider when deciding whether to fix a bug encountered during a refactor. First, it is far easier to verify that the refactor accurately replicates the original behavior if it is copied exactly, bugs and all. By fixing a bug while refactoring a section of code, we are decisively deviating from the reference behavior. Not only do we now have to consider the fixed bug when doing thorough regression testing of any kind, we also open ourselves up to introducing entirely new bugs or unexpected behaviors as a result of the bug fix.

## Clean up item

Keep track of everything that’ll need tidying, whether you plan to tackle the clutter at the end of your current milestone or only in the final stages of the project. Updating your list immediately as you render a section of code obsolete is critical; this way, you’ll be certain to remove each relevant artifact once you’ve reached the cleanup phase. The engineers who interface with the newly refactored code will be grateful for an orderly experience.

## Out-of-Scope Items

It would be better to just ignore it, if it affect timeline so much.

## Prototyping

When we set out to draft a plan for our refactor right level of detail. We wanted the plan to be approachable for important stakeholders who might not be intimately familiar with the technical details, but sufficiently specific that we could properly inform a team about the project and begin execution without ambiguity. Where the plan remained deliberately vague is a perfect opportunity for prototyping.

- Know that the solution might not be perfect
- Be willing to throw code away

## Keep things small

Please keep your commit small so it will easy to fix and track when something wrong happened

## Test Test Test

Creating a test when refactoring something is a must, there are no way you could do perfect reafactor without a perfect test.


