# Debugging a run or a customer complaint

Read the guide section `diagnosis` once before the first diagnosis of the session.

## 1. Follow the order
Follow the guide's "Diagnosing over MCP: the order": `setod_agent_health`, `setod_list_runs`,
`setod_read_run`, then the rest of its steps. Do not skip to a theory. A connector test in that
order can send a real message: ask a plain yes before it.

## 2. Read what the customer saw
For a customer complaint, read the conversation (`setod_read_conversation`, owners and managers)
or the staff request (`setod_get_staff_request`), and the run behind it, before saying what
happened. Quote the smallest part that explains the failure, and keep customer details out of
anything you write into Setod.

## 3. Quote the cause
Quote the step that shows the cause: the tool call, its arguments, its result. Say whether it is
an instruction problem, a tool that returned something unexpected, a missing connector or a
setting.

## 4. Check the known patterns
Read the guide section `failure_patterns`.

## 5. Propose one change, and say when it reaches customers
Propose one change and say why. On a live agent, say whether it reaches customers at once: skills,
notes, knowledge, links, triggers and reception settings are read live; instructions and most
settings wait for publish. The guide's "Live changes over MCP" lists the settings read from the
draft. Follow the yes rule in SKILL.md.

## 6. Reproduce, fix, run everything
Reproduce the failure as a scenario first, then fix, then run the whole suite
(`references/testing.md`).

## 7. Read-only tokens
A member or manager token, or a read token, can diagnose but not fix. Write the proposed change
for the owner and stop.

## 8. Final refusals
Some refusals are final from here: the guide's "Live changes over MCP" lists them, and any refusal
that says to do it in Setod is final too. Examples: a live run of an agent that can read hidden
data, a change to a hidden row, a code-skill test or an approval on a QuickBooks agent, a staff
request action on hidden data. Send the owner to Setod. Never detach, re-create, move, copy or
restore anything to get round them, and never ask a simulated agent to repeat hidden text.

## 9. Report
Tell the owner what you found, what you changed, what you tested and what is still open.
