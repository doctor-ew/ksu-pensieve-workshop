# Check shared memory before building

Proposed classroom feature, not a claim of an existing Pensieve capability.

Build a prior-art check. Given a short description of a task, search shared memory for
what other teams already decided or built, and return a cited report: each match with
its memory ID, who recorded it, when, and its status (current, superseded, or in
conflict with another match).

State what could not be checked. "Nothing found" means the search returned nothing; it
is never "no prior work exists." A failed or timed-out lookup is unresolved, not
"nothing found." The report is point-in-time.

Keep importing documents (for example Confluence pages), editing or deleting other
teams' memories, merging duplicate modules, and the decision to reuse outside the check.
A human decides what to reuse. Use synthetic fixtures (two teams that recorded
decisions about the same module) while learning.

Acceptance cases:
1. A relevant decision from another team is returned with its source, author and date.
2. Conflicting decisions are both shown and flagged, not merged into one answer.
3. A superseded decision is shown as superseded, never as current.
4. No match reports "nothing found," not "none exists," and never invents a match.
5. A failed or timed-out lookup is unresolved, not silently passed.

Ask Claude to inspect the existing search and provenance fields, propose a small spec
and tests, and identify assumptions before editing. Retain the requirement, source
revision, actual response, review decision, repair, and remaining limitation.

Source context: ../sources/AWS-SOURCE-EXCERPTS.md; src/aws-team-store.ts:16 (memory
rows carry contributor and creation time) and :139 (search). A superseded status is a
proposed field and does not exist in that source.
The acceptance cases above are authored teaching requirements.
