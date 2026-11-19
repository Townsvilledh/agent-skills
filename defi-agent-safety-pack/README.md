# DeFi Agent Safety Pack

Three skills that keep an AI agent honest when it touches DeFi money. They were written
from live failures — a refund stranded by an unverified route, fees hidden inside a
quote, a balance reported from a stale display — and each one forces the check that
would have caught the failure, before the agent reports or acts.

## Inside

1. **Disclose Fees by Component** — break every quote's total into its protocol,
   network and platform components, reconcile the parts against the total, and refuse
   the route when they disagree.
2. **Reconcile Wallet Balance Onchain Before Reporting** — read the exact chain balance
   for the exact address and contract before explaining any balance, failed send or
   swap; report the displayed figure and the chain figure side by side.
3. **Verify Settlement Behind a Contract Route** — a cheap contract call is not a
   route. Check who actually settles an order, whether a verified account or key gates
   assignment, and prove settlement with a measured test before calling a route
   permissionless or shippable.

## Who it is for

Anyone running an agent that quotes swaps, moves funds, reports balances or integrates
payment/escrow rails — and who cannot afford the agent inventing a number.

## Format

Three `SKILL.md` playbooks, one per folder. No code, no credentials, no network access
of their own: they discipline the tools your agent already has.
