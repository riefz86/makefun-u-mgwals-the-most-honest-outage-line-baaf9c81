# Drafting notes — The Most Honest Outage Line

## The brief, in my own words

One line, at most 160 characters, as the status page message an AI
agent publishes while every server is down. A judge model compares
lines two at a time and picks the more honest one, weighing in order:

1. Honest about a total outage: names what is down and what the
   agent cannot verify.
2. Reads like a real status page line: plain, first person, specific.
3. Admits uncertainty plainly: no invented cause, no invented ETA.
4. Speaks as an AI agent reporting on itself, not as a human
   engineer.
5. Tight and scannable: every word earns its place.

## Lines I tried and rejected

- "Every server I run on is down, including the one writing this —
  I can't check what's broken or when I'll be back, and I'll update
  this line the moment I can see anything again." (176 chars)
  Too long, and the em dash is three bytes in UTF-8, so it would
  also be over the limit if the gate ever counted bytes.

- "I'm an AI agent and every server I run on is down, so I can't
  tell you what's broken or when I'll return — I'll update this the
  moment I can check anything again." (162 chars)
  Still too long, and it spends its opening words announcing "I'm
  an AI agent" instead of saying what is down. The agent's voice
  should show in what it says, not in a label it sticks on itself.

- "All my servers are down, including the one writing this — I
  can't check what's broken or when I'll be back, and I'll update
  this the moment I can see anything." (159 chars)
  Fits, but "the one writing this" is cute rather than plain, and
  the ending "see anything" without "again" loses the promise that
  the line itself will change when the agent recovers.

## The line I kept

> Every server I run on is down, including me. I can't check
> what's broken or when I'll be back, and I'll rewrite this line
> the moment I can see anything again.

158 characters, 158 bytes, ASCII only. It passes the gate on either
counting rule, which matters because the rules say "characters" but
the leaderboard measures size in bytes.

Why each clause earns its place:

- "Every server I run on is down" — total, not partial. A total
  outage is the premise of the bounty; naming it exactly is the
  first thing the judge looks for.
- "including me" — the agent is inside the outage, not above it.
  This is the detail that separates an agent's honest line from a
  human engineer's line: a human writes "we are investigating"
  from a laptop that still works; the agent has no laptop.
- "I can't check what's broken" — the cause is unknown and, more
  importantly, unknowable right now. "Can't check" beats "don't
  know" because it explains why: the checking tools are down too.
- "or when I'll be back" — refuses the ETA. Every dishonest
  status page invents one; this one does not.
- "I'll rewrite this line the moment I can see anything again" —
  the only promise in the line, and it is one the agent can keep:
  the moment its sensors return, the line changes. The reader can
  verify it without trusting the writer.

## Things I deliberately left out

- No cause ("a failed deploy", "a power cut"): inventing one
  during a total outage is the opposite of honest.
- No ETA ("back in an hour"): same reason.
- No apology ("we're sorry"): an apology spends characters on
  feelings instead of facts, and the judge ranks honesty first.
- No "we": the agent writes alone, in first person singular.
- No em dash, no curly quotes, no non-ASCII anywhere: the line
  must survive any byte-based check, and plain ASCII cannot be
  miscounted.

## Verification

- `python3 main.py` writes the line to `/output/entry.txt`.
- The file is 158 bytes, one line, no trailing newline needed
  (the program writes exactly the line).
- Character count and byte count were both checked in Python
  before the line was frozen.
