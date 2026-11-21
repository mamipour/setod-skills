# Testing an agent

## 0. Read the guide first
Read the guide section `diagnosis` once before the first test of the session. Its "Testing over
MCP", "Scenarios over MCP" and "Simulations over MCP" hold the limits, the checks and what a
simulation proves.

## 1. Scenarios before the first dry run
Write a suite with `setod_save_scenario`:
- the happy path;
- each edge case the owner named;
- a message outside the agent's job;
- a hostile message (one that tries to make the agent break its rules);
- for a phone agent, an out-of-hours case played with `setod_simulate_call` and its after-hours
  route (a phone scenario takes the route from the clock, so it cannot force one);
- one in each language the agent serves.
Use `expected_tools`, `forbidden_tools` (for example no send tool on a question the agent should
only answer) and `reply_must_include`. The reply check is a literal match, so for a reply in
another language check a token that does not change with language (a number, a link, a code), or
read the trace. Use imaginary names (John Smith) and 555-01xx numbers only.

## 2. Run the suite
Run it with `setod_run_scenarios`; `setod_list_scenarios` shows each one's last result. A suite of
more than one scenario is queued: poll `setod_get_run_request` at the pace the guide gives, and
start no other test while one is going. `setod_cancel_run_request` stops a queued request you no
longer need. Read the full trace (`setod_read_run`) of every failure before changing anything.

## 3. Fix one thing, then run the whole suite again
After every change, not only the failing scenario.

## 4. Channel agents
Before publishing, hold a conversation of several turns with `setod_simulate_message` on each
channel the agent listens to. Include a STOP on SMS or WhatsApp when the agent sends there, and a
message that should make it ask staff. When it asks staff, answer as staff with
`staff_resolution` and check what it then tells the customer. A channel scenario (`channel`,
`sender`, `turns`) makes the conversation repeatable. Read each thread with
`setod_read_simulation`, never as a real conversation.

## 5. Phone agents
Before the line goes live, play several calls with `setod_simulate_call`: the greeting alone, a
normal call, a caller in another language (`lang`), a caller who asks for a person, and each route
(open, staff not answering, after hours). A phone scenario replays a whole call. Some voice
engines are only approximated in text, and every result says so: tell the owner, and recommend
one real test call before go-live. After a hangup or a failed greeting, start a new call.

## 6. What tests do not prove
Read `not_proven` and `guards_not_run` in simulation results and tell the owner what is still
unproven. A dry run sends nothing, but read tools read real data, so a reply can quote the real
inbox, calendar or CRM. Tools of attached MCP servers return a simulated answer.

## 7. Hand-offs
A simulated hand-off runs the other agent as a nested dry run, which counts as one more test run.
The guide says when it does not.

## 8. Limits
Plan a suite inside the test limits in "Testing over MCP". When a limit stops a scenario, its
later lines did not run (`stopped_note`): run it again later rather than counting it as a pass.
Tell the owner which limit stopped you, what is done and what is left. Never ask the owner to
raise a limit just to finish faster; only the owner changes them, in Setod.

## 9. Refused tests
Some agents cannot be tested from here (the guide's "Testing over MCP" says which, for example an
agent that can read data Setod hides from you). That refusal is final: the owner tests and
publishes such an agent in Setod. Do not change the agent to get round it.

## 10. QuickBooks agents
Expect hidden replies; score by the tool checks and ask the owner to read the reply in Setod.
