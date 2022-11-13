# Part 2 Planning

Refactoring also need some planning

## Why Is Measuring the Impact of a Refactor Difficult?

Large refactoring efforts are particularly difficult to measure because they rarely take
place in the span of just a few weeks.

- Benefit may only seem for developer productivity
- Some behaviour not documented properly

## Measuring Code Complexity

### Halstead Metrics

Maurice Halstead first proposed measuring the complexity of software in 1975 by counting the number of operators and operands in a given computer program. He believed that because programs mainly consisted of these two units, counting their unique instances might give us a meaningful measure of the size of the program and therefore indicate something about its complexity.

- A program’s volume, or how much information the reader of the code has to absorb in order to understand its meaning.
- A program’s difficulty, or the amount of mental effort required to re-create the software; also commonly referred to as the Halstead effort metric. 
- The number of bugs you are likely to find in the system.

### NPath Complexity

NPath complexity was proposed as an alternative to existing complexity metrics in 1988 by Brian Nejmeh. He argues that focusing on acyclic execution paths did not adequately model the relationship between finite subsets of paths and the set of all possible execution paths. We can observe this limitation in the fact that cyclomatic complexity does not consider nesting of control flow structures. A function with three for loops in succession will yield the same metric as one with three nested for loops. Nesting can influence the psychological complexity of the function, and psy‐chological complexity can have a large impact on our ability to maintain software quality.

## Lines of Code

Unfortunately, control flow graph metrics can be difficult (and sometimes expensive) to calculate, particularly for very large codebases (which are precisely the ones we’re looking to improve). This is where program size comes into play. Although it may not be quite as scientific as Halstead, McCabe, or Nejmeh’s algorithms, combined with other measurements, program size can help us locate likely pain points in our application. If we’re looking for a pragmatic, low-effort approach to quantifying the complexity of our code, then size-based metrics are the way to go.

- LOC (line of code)
- Function Length
- Average function length per-file


## Test Coverage Metrics

When we’re developing new features, there are a few testing philosophies we can adopt. We can opt for a test-driven development (TDD) approach, writing a thorough suite of tests first and then iterating on an implementation until the tests pass; we can write our solution first, followed by the corresponding tests; or we can decide to alternate between the two, incrementally building an implementation, pausing to write a handful of tests with each iteration. Whatever our approach, the desired outcome is the same: a new feature, fully backed by a quality set of tests.

## Documentation

A program can be easily refactored if there are docs.

- UML
- PRD
- Database Graph/Design
- API Docs

Typed language can reduce the amount of time we refactor code.

## Version Control

We primarily think of version control as a tool to manage changes to our applications. We use it to move forward incrementally, allowing for the development of multiple features at once, and progressive shipment of those features. Sometimes, we use it to refer to previous versions of our code to track down a bug or locate someone who might know about the section of code we’re reading. We rarely think of version control as a source of information about our team’s development patterns when analyzed in aggregate. Turns out, we can glean quite a bit about the problems our engineering team is facing when we take a look at our commits from a different perspective.

### Commit Message

Measuring code complexity can be done in commit message

### Commits Aggregate

We can apply the same concept of change frequencies to files as well. By looking at individual commits, we can carefully attribute changes to respective functions within individual files, producing total frequency numbers for each of them. By combining this data with one of our earlier complexity metrics, lines of code, we can map complexity changes over time across the entire codebase. This information shows us potential hotspots ripe for improvement. We can later regenerate these metrics once we’ve completed our refactor to confirm that not only the complexity of these hotspots decreased, but hopefully their change frequency had as well.

## Reputation

Software have some reputation in every part of it. There are some part of a software that are positive and one that are not. We can meausure it by asking some question.

- How long you have been working on X?
- If you can change one thing when working on X what it would be? Why?
- Tell me about bug you recently had to fix?
- Have you avoided working with X code before?
- How the complexity of X hinder you from developing new features?
- Does the complexity of X can hinder your ability to test and debug?
- How does the complexity of X hinder your ability to review other developer work/PR?

## Drafting A Plan

We should define our end state.

- Mapping the shortest distance, we should know what plan are the most quick to implement.
- Write down every step of the refactoring carefully, from where we should start
- Gather some coworker who might be interested in the project
- Evaluate every step what are the direct impact? Is it good for DX/Bussiness?
- Create a backup, in case we screw up.
- Create a rollout strategy, better refactoring should be deployed step by step

## Cleaning Up Artifact

- Check if every comment still okay
- Check if the code are still used, if not just remove it (remove dead code)
- Use feature flag to rollout
- Shield our refactor from other developer by using an abstraction
- Check if the unit test still used, if not remove it.

## Avoid Scope Creep
> While other teams’ ideas and outlooks are incredibly helpful in finalizing our execution plan, we have to continue to focus on our ultimate goal so as not to introduce any additional scope accidentally. There might be a handful of small, new steps we need to add to our plan to handle an edge case or two properly that we hadn’t previously considered; however, we should be careful to add only what is absolutely necessary to ensure that we can reach our desired end state while maintaining our major milestones.
