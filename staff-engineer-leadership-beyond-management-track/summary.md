# Overview

## Staff engineer archetypes

- **Tech Lead** guides the approach and execution of a particular team.

- **The Architect** is responsible for the direction, quality, and approach within a critical area. They combine in-depth knowledge of technical constraints, user needs, and organization level leadership.

- **The Solver** digs deep into arbitrarily complex problems and finds an appropriate path forward. Some focus on a given area for long periods. Others bounce from hotspot to hotspot as guided by organizational leadership.

- **The Right Hand** extends an executive’s attention, borrowing their scope and authority to operate particularly complex organizations. They provide additional leadership bandwidth to leaders of large-scale organizations.

## Tech Lead

- Manage/Tackle blocking task when required
- Delegating task
- Scoping task with PM
- Mentoring

## Architect

- Responsible for success of a specific technical domain.
- Maintaining intimate understanding of the business need and relevant constraints.
- Advocate for effective approach within their area of focus


## Solver

- The one who dabble with hard problem and doing it until it resolve (tech debt, etc)
- Solver operate in already identified problem (bugs, upcoming complexity)

## Right Hand

- Senior without direct managerial responsibilities
- Right hand dive into fire, edit the approach, delegate execution to the most appropriate team, and jump to the next fire

## Which are the right for you?

Choose something that energize you, you can discover it late or soon, it's different because of company size or culture.

## What do Staff engineer actually do?

> The role of a Staff-plus engineer depends a lot on what the team needs and also what the particular engineer’s strengths are. From my experience, the responsibilities of a Staff-plus engineer can change over time. Still, usually, their main focus is working on projects/efforts that have strategic value for the company while driving technical design and up-leveling their team. - Diana Pojar

Keep doing much of what made them successful as Senior Engineers

- Building relationship
- Writing software
- Coordinating projects

But now it is auxiliary task, not the main task. But there are shared foundation on it

- Setting and editing technical direction
- Providing sponsorship and mentorship
- Injecting engineering context into organizational decisions
- exploration
- being glue ~ https://noidea.dog/glue

## Setting technical direction

Understand and solving the real needs, experiment after experiment.

## Mentorship and sponsorship

You’re far more likely to change your company’s long-term trajectory by growing the engineers around you than through personal heroics.

Sharing your experience and advice.

https://larahogan.me/blog/what-sponsorship-looks-like/

## Providing engineering perspective

Effective orgs streamline routine decision making. Staff engineer will often get unexpectedly pulled into the room where something need discussion happen.

Just remember that you're representing the interests of all engineering, not just your own.

## Exploration

Prototyping, care towards DX. Always try something that improve company business.

## Being Glue

Doing the needed, but often invisible task to keep the team moving forward and ship.

## Will you still write software?

It depends. You should still remember that your decision should based on-the-ground experiences to the rest of your team.

More of the job will be about mentoring and growing people around you. Sometimes it's hard to metric.

## Slow but rewarding

Timeframes are longer. 

## Does title even matter

- Allowing you to bypass informal gauges of seniority
- Facilitating access to the room
- increase current and career compensation
- Grant more freedom/agency

When you have a title, you don’t have to spend so much energy putting your credentials on the table. It helps set the context for others. You’re more respected from the outset, and that’s been really noticeable.

## Access to interesting work

Might get you access to some interesting project

## Different rather than better

## Material but not magic

Attaining certain title isn't the only thing standing between important and not important people.

# Operating at Staff

## Topics

- Work on what matters
- Write an engineering strategy
- Curate technical quality
- Stay aligned with authority
- To lead you have to follow
- Learn to never be wrong
- Crate space for others
- Build a network of peers

You can’t escape subjective interview practices, but you can deliberately accumulate expertise from doing valuable work. Indeed, that’s the only viable long-term bet on your career: focus on work that matters, do projects that develop you, and steer towards companies that value genuine experience.


## Write an engineering strategy

- Start from the problem
- Keep the template simple
- Gather and review together, write alone
- Prefer good over perfect

Synthesize design docs into strategy. Writing strategy document

- Start where you are
- Write the specifics
- Be opinionated
- Show your work

Extrapolate five strategies into a vision.

- Write two to three years out
- Ground in your business and your users
- Be optimistic rather than audacious
- Stay concrete and specific
- Keep it one to two pages long

## Managing technical quality

Low technical quality it's the expected normal state.

- Fix the hot spots that causing immediate problem
- Adopt best practices that known to improve quality
- Prioritize leverage points
- Align technical vectors
- Measure technical quality
- Spin up technical quality team
- Quality program

Do the quick stuff first, even if it doesn't work.

## Best practices

It's awkward to acknowledge mistake, but it will be better of. 

Good process evolved rather than mandated. Study how other companies adopt similar practices, document the approach. Rushed process is failed process.

Better for early adoption :

- CI/CD
- VCS
- Trunk Based Development
- Production Observability
- Better internal docs

## Leverage Points

- Give direct feedback
- Refine your engineering strategy
- Encapsulate your approach in workflow and tooling
- Train new team members during their on boarding
- Use conway law, org build software that reflect their structure.
- Curate technology change

## Measure technical quality

- What percentage of the code is statically typed?
- How many files have associated tests?
- What is test coverage within your codebase?
- How narrow are the public interfaces across modules?
- What percentage of files use the preferred HTTP library?
- Do endpoints respond to requests within 500ms after a cold start?
- How many functions have dangerous read-after-write behavior? Or perform unnecessary reads against the primary database instance?
- How many endpoints perform all state mutation within a single transaction?
- How many functions acquire low-granularity locks?
- How many hot files exist which are changed in more than half of pull requests?”

Operating teams :

- Trust metric over intuition. You should have a way to measure something dont use intuition
- Keep your intuition fresh
- Listen to and learn from your users
- Do fewer things, but them better.
- Don't hoard impact, balance the benefits of exploration against the benefits of standardization.

## Quality program

A quality program isn’t computer code at all, but rather an initiative led by a dedicated team to maintain technical quality across an organization.

- Identify a program sponsor
- Generate sustainable, reproducible metrics
- Identify program goals for every impacted team and a clear path for them to accomplish those goals
- Build docs and tools to support teams towards their goals
- Create a goal dashboard and share it widely
- Send programmatic nudges for folds behind on their goals. Attract people to take towards your program goals.
- Periodically review program status with your sponsor

Leading cause of failed program

- Running it purely from process perspective and detached from reality.
- Running it purely from technical perspective and skipping essentials steps
- trying to cover those perspective as a single person

## Start small and slowly


