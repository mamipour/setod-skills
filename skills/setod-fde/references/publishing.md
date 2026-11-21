# Publishing and going live

Every step here reaches real customers or a real phone number. Follow the yes rule in SKILL.md:
the owner's earlier request to publish or go live does not stand in for the yes to your question.

## 1. Channel listeners, saved before publishing
Read the guide section `lines` before any channel step. Save each listener on the draft with
`setod_set_channel_trigger` before you publish: a listener on a draft answers nobody, and goes
live with the publish. Call it with no string; if it is refused, show the owner the reasons (for
example who else answers that channel, or where a bot delivers today and what is lost by moving
it) and ask. When two agents would answer the same channel, say so plainly.

## 2. Before publishing
Check that:
- the scenario suite passes, or the owner accepted each failure you explained;
- channel or phone simulations were run (`references/testing.md`);
- `setod_validate_agent` is clean;
- a dry run of the current draft (`setod_run_agent` with `dry_run` and `use_draft` true)
  succeeded recently. The server checks the window and refuses otherwise.
Then call `setod_publish_agent` with no string. Its refusal lists the publish warnings (another
agent on the same channel, a line that does not point at the agent, numbers a role agent's publish
would move) and any second string it needs. Show the owner the dry-run report, the warnings, each
listener and who it will answer, and what will go live, by name, then ask one question. On a yes,
call it again with the strings the refusal asked for.

## 3. What publish freezes
Instructions, model and most settings; the guide's "Live changes over MCP" lists the settings read
from the draft. Connectors, skills, code skills, knowledge, notes, links, triggers and reception
settings are read live on every run, published or not.

## 4. Phone lines, their own step after publish
Read the guide section `lines` first. A role agent is different: its numbers move when it is
published, so the publish question names each number and who answers it now. For other agents,
`setod_set_phone_trigger` saves the voice settings and never moves the number, and
`setod_phone_go_live` points the number at the agent: call it with no string, and its refusal
says who answers the number today. Tell the owner, by name, who will stop getting the calls, then
ask. If the owner wants the line live before the agent is published, say what callers get
meanwhile, as the refusal and the guide describe it.

## 5. Live runs
Only when the owner asked for one, and still as a gated call: call with no string, show the
reasons, ask, and only on a yes pass `RUN LIVE`. Start it with `wait=false`, then poll
`setod_get_run_request`.

## 6. Watch the first live runs
Offer to read the agent's health, its recent runs and the first conversations or calls after
going live, and report anything that failed. Reading needs no yes.

## 7. The way back
Before going live, name the way back: roll back to the previous version, pause, or detach the
line. Each of these is itself a live change and takes the owner's yes.
