# Agent Work Verification Pack

Two skills for anyone who delegates work to agents — subagents, scheduled jobs, or
outside builders — and needs to know the work actually happened.

## Inside

1. **Verify Delegated Build Claims** — never repeat a builder's report as fact.
   Re-derive the claim on the live product, use independent ground truth (a second
   library, an official test vector, an on-chain read), pin the exact path the user
   touches, and report only what you proved.
2. **Prove Scheduled Work Completed** — a clean exit code is not proof. Check what the
   run changed in the world, write a completion record on every run, watch the pulse
   from outside the job, and report skips as skips.

## Who it is for

Agent operators and orchestrators who have been burned by a confident report that
nothing checked — a deploy that never landed, a cron job silently skipping for days,
a "fixed" flow nobody walked.

## Format

Two `SKILL.md` playbooks, one per folder. Process discipline, not code: they change
what your agent verifies and reports, using the tools it already has.
