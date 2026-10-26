## Rules

- End a task with a summary that has one section per request, headed by the outcome the user sees ("Expired cards are rejected before payment"), not by the code change.
- In each section, say what the code now does and why that works, with its `file:line`. Name anything else the change forced (a dependency, a config flag) and every other caller that gets the same change.
- List each scenario or edge case the change handles as its own one-line bullet with a bold label (**Card expires mid-checkout:** ...).
- For a bug fix, reproduce each distinct case before changing code, run the same cases again after the change, and show both results in a table.

  | Case                     | Before                         | After                       |
  | ------------------------ | ------------------------------ | --------------------------- |
  | Expired card             | Sent to the provider, declined | Rejected with `402`         |
  | Card expiring this month | Accepted                       | Accepted                    |
  | Missing expiry date      | Server error (`500`)           | Rejected with `422`         |

- State the evidence: what was run and what was observed (test output, exit codes, timings, the state the system ended in).
- Close with what was not verified (a check that could not run, a platform not tested) and anything unexpected that happened during the work.

## Anti-patterns

- NEVER report a result that was not observed — mark inferences and untested cases as such.
- NEVER put a failed or skipped check below the successes, where it gets missed.
