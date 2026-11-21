# Building an agent

Read the guide section `tools` once before the first build step of the session. The guide's
"Building blocks over MCP" names the tool for each block and when it needs the owner's yes.

## 1. Understand the job before touching anything
Ask what the agent is for, who it talks to, on which channel or phone line, in which languages,
what it must never do, and who answers when it is unsure. Then read what is there:
`setod_workspace_overview`, `setod_list_agents`, `setod_list_connectors` and `setod_get_roster`.
A hired role, or a role that fits the job, is often better than a custom agent: reception roles
are set up as in `references/reception.md`. Reuse an agent or a template when one fits.

## 2. Connectors first
A missing connector is added by the owner. `setod_connect_link` gives the link to the place in
Setod where the owner enters the sign-in or key. Never ask for the credentials, and never type
them for the owner. Ask the owner to tell you when it is done, then check `setod_list_connectors`
until the connector shows active. Check at a calm pace, not in a tight loop; if it is still not
active after a few checks, ask the owner what they see.

## 3. Build order
Prefer, in this order: a tool of an existing connector, then a prompt skill from the library,
then a code skill, only for mechanical work the model does badly (parsing a feed, date maths, an
API with no connector). Put facts that change in knowledge, records in tables, and short live
facts in owner notes. Before the first row write of the session to a table a live agent reads,
name those agents and ask a plain yes.

## 4. The draft agent
Create it with `setod_create_agent` and change it later with `setod_update_agent`. Pick the model
from `setod_list_models` (the workspace's own key) or `setod_list_platform_models` (models Setod
manages), never an invented name. Take settings only from `setod_get_settings_schema`, and read
`dropped_settings_keys` in the answer: a key listed there was not saved.

## 5. Instructions
Plain English, short, inside the guide's advice in `prompt_rules`. No tool syntax, memory keys or
regex, and no rule a skill already covers. For languages, one English line such as "Reply in the
language the customer writes in." Before you overwrite instructions the owner wrote, show what
changes and ask a plain yes.

## 6. Code skills
`setod_create_code_skill`, then `setod_deploy_code_skill`, then check `setod_get_code_skill` until
it is ready or failed, then `setod_test_code_skill`, then attach it. A skill that only fetches or
parses must be `read_only`, or a dry run proves nothing. Mark a skill `read_only` only when it
changes nothing outside Setod: no writes, posts, sends or payments. Tell the owner that a
`read_only` skill runs for real in every dry run and simulation: it uses the workspace's
code-skill quota and calls outside services. A test runs the code for real: before
`setod_test_code_skill` on a skill that can reach outside services and is not `read_only`, say what
it will do and ask a plain yes. Secret values are entered by the owner: `setod_list_code_skill_secrets`
gives the names and the link.

## 7. Knowledge
Check the file's size against the guide's limit before an upload; a larger file goes through the
agent's Knowledge tab, by the owner. After an add, check `setod_list_knowledge` until the file is
ready or shows an error. Before any retry, check the list again: a retry can add the same file
twice.

## 8. Triggers
A schedule can be added to a draft safely. Read the guide section `lines` before a channel or
phone step. A channel listener is saved on the draft and goes live with the publish; a phone line
goes live in its own step after publish (`references/publishing.md`). Role agents get their
channels and lines from their Playbook answers, never from the trigger tools.

## 9. Validate
Run `setod_validate_agent` and fix every problem it reports before the first test.

## 10. Then test
Follow `references/testing.md` before anything is published. Tell the owner what you created and
changed so far; additive work on a draft needs no yes, but say what it was.
