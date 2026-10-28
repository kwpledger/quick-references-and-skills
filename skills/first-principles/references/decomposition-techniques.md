# Decomposition Techniques

Read the section that fits the problem; you rarely need all of them.

- Problem-type split: untangling several problems that arrive as one
- Enhanced why-chain: finding root causes
- Function ladder: opening up the solution space
- Component mapping: separating function from implementation
- Cost and effort decomposition: when something is "too expensive" or "takes too long"
- Hard-limit check: physical, technical, and human limits
- Synthesis: rebuilding from what's left

## Problem-type split

When a problem feels overwhelming and shapeless, it is often several problems of different kinds. Sort the pieces before decomposing any of them:

| Type | Shape | What solves it |
|---|---|---|
| Removal | One-time backlog | Timeboxed sprints with simple decision rules |
| Organization | One-time structure | Giving each thing a home or a slot |
| Flow | Ongoing rate | Matching output to input: smaller, more frequent cycles |
| People | Ongoing coordination | Clear ownership, visible cues, done-definitions |

**Example: a cluttered apartment, a laundry mountain, and no chore system.**

- **Removal:** clutter that should leave the apartment or go to storage.
- **Organization:** closet and dresser zones, so everyone's clothes have a visible place.
- **Flow:** laundry arrives daily, so a weekly batch always piles up.
- **People:** who owns which chore, and how they're reminded.

Sequence: organization first, because laundry can't flow back to a place that doesn't exist. Then flow and people. Removal last, in sprints, since clearing a backlog while the flow is broken just rebuilds the pile.

The same split works outside the home. An overflowing inbox has removal (old mail), organization (folders or rules), flow (daily volume), and people (who should be getting those messages instead).

## Enhanced why-chain

A standard "5 Whys" usually stops at an operational cause. Keep going until you reach bedrock (see SKILL.md, Step 2).

```
Levels 1-3: operational causes (what's happening)
Levels 4-5: systemic causes (why the system produces it)
Level 6+:   bedrock (physics, logic, hard rules, or the user's own values)
```

**Example: new hires take six months to become productive.**

1. Why? The onboarding course is 40 hours of slides and they forget most of it.
2. Why slides? They're the fastest format to build and update.
3. Why must it be fast to update? Procedures change every quarter.
4. Why does the course carry procedure details at all? It doubles as the procedure reference.
5. Why? No separate, controlled reference exists.
6. **Bedrock:** People need (a) a mental model of the system and (b) current procedure details at the moment of work. Memory doesn't retain 40 hours of detail, and the details change anyway. The course is serving two functions and doing both badly.

The fix that falls out (teach the model, point to a living reference for details) was invisible at level 1.

Stop early when the next "why" wouldn't change what you'd do.

## Function ladder

Climb from the stated function toward the underlying need. Each rung up opens more options.

```
Stated:      "I need a faster car for my commute"
Deeper:      get to work in less time
Deeper still: reclaim time and energy lost to the commute
Need:        more usable hours in the day

Options that appear only higher up:
├── shift work hours to miss traffic
├── negotiate remote days
├── make commute time usable (transit + reading, audio learning)
└── move closer (expensive, but now visible as an option)
```

Climb only as high as the user's real goal. Going higher than they care about produces options they'll never take.

## Component mapping

List the parts of the current solution, then separate what each part does from how it does it.

| Component | Function | Function needed? | Other ways to do it |
|---|---|---|---|
| Slide deck | Convey concepts | Yes | Simulation, demo, worked examples, job aid |
| Final quiz | Verify competence | Yes | Performance check, scenario in a sim, supervisor sign-off |
| 40 hours of seat time | Satisfy a requirement | Check: is the rule hours, or demonstrated competence? | If competence, time can shrink |

The insight: the function is usually fundamental; the implementation almost never is. Watch for components whose "function" is really a firm constraint in disguise, like seat time.

## Cost and effort decomposition

For "too expensive" or "takes too long":

```
Total = Σ (input × quantity) + process + overhead + margin/buffer

For each line:
├── Is this input necessary?        (function)
├── Is this quantity necessary?     (efficiency)
├── Is this process step necessary? (process)
└── Is this margin necessary?       (who is it protecting?)
```

A quick test: compare the price of the finished thing with the cost of its raw inputs. A contractor quotes $12,000 for a deck; lumber and hardware run $3,500. The $8,500 gap is labor, overhead, margin, and risk, and each piece can be examined separately. Some of it is real (skilled labor, permits). Some may be soft (a padded timeline).

The same works for time: a report that "takes a week" might be four hours of analysis plus four days of waiting on approvals.

## Hard-limit check

Before accepting a rebuilt solution, check it against the limits that apply to the problem.

**Physical and technical problems**
- Conservation of energy and thermodynamic limits
- Realistic material properties
- Information and bandwidth limits
- Scale effects (square-cube law: doubling size doesn't double strength)
- Hardware ceilings (compute, memory, storage throughput)

**Human and organizational problems**
- Attention and working memory are limited; people can hold only a few new items at once
- Hours in a day, and recovery time after focused work
- Skill takes practice time to build, regardless of how good the material is
- Every handoff between people adds delay and error

If a solution breaks one of these, it isn't a solution.

## Synthesis

After decomposing, rebuild deliberately:

1. List the verified bedrock: hard constraints, firm constraints with their costs, and the user's values.
2. Define the minimum function: what must the result do?
3. Generate options for each function without filtering.
4. Evaluate the options against bedrock only, not against "how it's usually done."
5. Combine the best options into one approach.
6. Check it against the original outcome statement from Step 1.

Build up from what's true instead of trimming down from the existing solution. Trimming keeps the old structure's assumptions intact.
