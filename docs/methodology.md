# Methodology

These are the rules every published result follows. A result that breaks one of them is not published as a comparison; it is published as a declared exception, or not at all.

## The rules

1. **Same task, same data, same machine.** Every engine in a lane answers the same queries over the same corpus on the same dedicated machine. The machine's specification is on the results page.
2. **Answers are checked.** Each query's answer is reduced to a digest and compared between engines. A fast wrong answer is a failure, not a result.
3. **Settings are published.** Each engine runs at its documented defaults unless a setting is required to run the task (a memory limit, a durability class, an index the task needs).
   Every deviation is listed on the [Engines](engines.md) page with the reason. An index added for one engine is added, in its equivalent form, for every engine that has one.
4. **Equal resources.** Every engine gets the same memory cap and CPU allotment inside a lane, and the same durability classes are measured for every engine that offers them
   (a relaxed class and a strict class where the engine supports both).
5. **Repetitions and medians.** Each cell is run several times (at least three), and the page prints the median with its spread, never a single run.
6. **Budgets and censoring.** A query that cannot finish within its time budget is recorded as censored, with the budget, and is never silently dropped or counted as fast. Where an engine
   can be asked to stop a query itself, the budget is enforced by the engine; otherwise it is checked between iterations.
7. **Failures are results.** An engine that runs out of memory, times out or refuses a task has that recorded as its result for the cell, with the error it gave.
8. **Versions are exact.** Every row records the engine version and, for containers, the image digest it ran on. A cell never mixes rows from different versions: when an engine ships a new
   version, new rows are added next to the old ones.
9. **Warm-up is declared.** Whether a timing includes the first run, a warm-up, or an index build is stated in the table it appears in.
10. **History is kept.** A correction or a new version adds rows; the earlier rows stay visible.

## Reading a result

A bar or a number is only meaningful with its footnotes: the category (in-process or server), the durability class, the scale, the version, and whether any query in the cell was censored.
The results page carries all of these next to every number.

## What this benchmark does not claim

It does not rank databases in general. It measures the tasks listed in each lane on the stated machine and settings. A different workload, scale or tuning can change the order, which is why
the settings are published and why vendors are asked to review them.
