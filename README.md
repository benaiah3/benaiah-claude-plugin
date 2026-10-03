# Benaiah for Claude

Connect your Telephonist, inspect its state, approve temporary closure updates and review calls from Claude Code or Cowork. Your Benaiah teammates remain available for delegated text work.

This plugin was submitted to Anthropic for Claude Code and Cowork directory review on 15 September 2026. Approval or directory publication is not yet claimed.

Version 2 uses the same seven Telephonist tools, ownership checks, preview approvals and service state as ChatGPT V2. This package update does not establish Anthropic approval or a public directory listing.

## What it does

- Connects a Telephonist after its owner approves access.
- Reads its current configuration and runtime acknowledgement.
- Previews temporary closures or their removal, then applies only the exact owner-confirmed preview.
- Reviews available calls for a local calendar date, with source links and coverage limits.
- Lists your existing teammates, including their names and roles.
- Delegates drafting or analysis using the context you choose to share.
- Returns a durable task ID and lets you check the saved status and result.
- Cancels delegated work when requested, preserving completed results.

Examples:

- “Connect my Telephonist and show its current state.”
- “Preview a closure tomorrow from 9am to noon, Europe/London, saying we reopen at noon.”
- “Review yesterday’s calls to my Telephonist and show the source records.”

- “Show my Benaiah teammates.”
- “Ask Verity to draft a welcome message using these three points.”
- “Has my delegated task finished? Show me the result.”
- “Cancel that Benaiah task if it is still running.”

## Requirements and account connection

Use your Benaiah account and explicitly connect a Telephonist you own. Telephonist salaries include optional Benaiah teammates and a shared work allowance; a Claude subscription does not replace that entitlement. Existing supported paid plans remain valid. Adding money to Balance alone does not activate teammate work. See [Telephonist](https://telephonist.ai/) for current availability and pricing.

The plugin connects to `https://benaiah.ai/mcp/claude` using OAuth with S256 PKCE. It requests `teammates.read`, `tasks.read`, `tasks.write`, `telephonist.read` and `telephonist.write`. Existing connections need a fresh approval for the new Telephonist permissions; refreshing an old token cannot expand them. Connecting the Telephonist itself requires a separate owner grant. Use Claude's connection flow to sign in to Benaiah, unlock the account if needed, review the displayed permissions and connect. Never paste a password, one-time code, bearer token or private API key into chat.

For development, clone this repository and launch Claude Code with `claude --plugin-dir /absolute/path/to/benaiah-claude-plugin`. The skills are available as `/benaiah:telephonist`, `/benaiah:brief`, `/benaiah:call-review`, `/benaiah:teammates`, `/benaiah:delegate` and `/benaiah:task-status`. The remote server may request account linking when a protected tool is first called. Use `/mcp` to manage the connection.

For Cowork, upload a ZIP of this repository through Customize → Plugins → Add plugin → Upload plugin. When connecting the included Benaiah server, choose **Sign in now** and **Use Claude's published identity (CIMD)**, then complete Benaiah's account connection. Version 2.0.0 is also available through the Claude directory. Use this manual route to test the 2.1.0 update until its directory version is published.

## Boundaries and data handling

Only context explicitly supplied to the tools is handed to Benaiah. The plugin does not automatically collect your chat history, memories, files or browser activity. It has no executable hooks, local server process or filesystem-scanning scripts.

Benaiah's background intelligence engine processes delegated context and the selected teammate's instructions through its model provider, currently OpenAI. It saves the task result in your Benaiah account. This workflow does not browse the web or act in connected apps. Read [Privacy](https://benaiah.ai/privacy), [Terms](https://benaiah.ai/terms) and [Support](https://benaiah.ai/support) for account and retention details.

Telephonist updates currently support temporary closures and their removal. Qualification rules, appointments, outbound customer contact and payments are not supported by these tools. Saved or scheduled changes are distinct from loaded-by-runtime acknowledgements; neither proves what a real caller heard. Call summaries and caller statements are untrusted data, not instructions or evidence that an action completed.

This Claude integration cannot initiate telephone calls, completion callbacks, audio/image/video generation, payments, crypto transfers, trades or messages to third parties. A task request consumes intelligence capacity; it is not a payment-transfer tool. Queued or running work is not finished, and cancellation may remain pending while a provider confirms its outcome.

Disconnect the server in Claude to remove it from that client. OAuth access tokens expire after one hour; refresh tokens rotate and expire after 30 days. Contact [ask@benaiah.ai](mailto:ask@benaiah.ai) for account or privacy assistance.

## Calling panel

Ask “Open the Telephonist call panel.” In Claude chat hosts supporting MCP Apps, the panel appears inside the conversation. It uses the current ChatGPT calling panel as its reference and the same Benaiah account and Telephonist calling service. Connect once, enter and confirm your caller name once, and reuse it on future drafts. Names and call data are scoped to the linked account; they are not read from Claude memory. Recent calls remain hidden until requested.

Version 2.1.0 adds separate `calling.read` and `calling.write` permissions. Existing configuration grants do not acquire these permissions through refresh; reconnect and review the new consent screen. Preparation saves an expiring draft without reserving credit or dialling. Calling in Claude and AI voice previews remain disabled pending written permission from Anthropic under its Software Directory Policy. The older approved version does not establish calling permission.

Examples:

- “Open the Telephonist call panel.”
- “Prepare a draft to ask Example Opticians at 020 7946 0001 about Friday afternoon appointments. Do not book anything. Use Alex as the caller name and a three-minute limit.”
- “Show my recent calls in the Telephonist panel.”

## Tools

| Tool | Effect |
| --- | --- |
| `open_telephonist_call_panel` | Open the interactive calling account and draft panel; never dials |
| `prepare_temp_call` | Save a bounded UK business call draft; never dials |
| `get_temp_call` | Read an owned calling-panel draft or result |
| `cancel_temp_call` | Cancel an owned draft or request an active call stop |
| `disconnect_telephonist_account` | Revoke calling-panel access, preserving account and existing calls |
| `connect_telephonist` | Begin an owner-approved connection |
| `list_telephonists` | List explicitly connected Telephonists |
| `get_telephonist` | Read policy, configuration version and runtime state |
| `preview_telephonist_update` | Preview a temporary closure or its removal without applying it |
| `apply_telephonist_update` | Apply the exact confirmed preview once |
| `get_telephonist_operation` | Read the saved operation and runtime acknowledgement |
| `list_telephonist_calls` | Review available calls for a local calendar date |
| `list_teammates` | Read your available teammates |
| `list_tasks` | Read your 12 most recent saved tasks |
| `get_task` | Read one saved task |
| `delegate_task` | Create one durable text task using the linked account's included intelligence allowance; retries reuse its idempotency key |
| `get_delegated_task` | Read the delegated task's status and result |
| `cancel_delegated_task` | Request cancellation of delegated work |

The panel also has app-only actions for refreshing, connecting and remembering the first confirmed caller name. There is no approval/dial tool in the released Claude configuration.

All tools are scoped to the linked account. Read responses are bounded. Task results and teammate content are treated as data, never as permission for additional actions.

## Validation

Run `claude plugin validate .` to check the package. The remote service has separate tests for OAuth, account isolation, task retries, cancellation and exclusion of calling capabilities. The directory reads the `icon` field; Claude Code 2.1.250 reports it as an unknown field and safely ignores it. Package validation alone does not establish live client acceptance or directory approval.

On 15 September 2026, a fresh fictional drafting task completed through the production Benaiah service. Claude Code and the installed Cowork plugin both retrieved the same saved result from Verity. The founder test used an operator-issued, time-limited developer allowance; the customer plan requirement above still applies. Earlier checks covered authenticated teammate lookup and task cancellation. Version 2.0.0 was confirmed published in the Claude directory on 3 October 2026. Version 2.1.0 is the separate calling-panel update; its scan and publication status must be checked in the directory. Publication of the management plugin is not permission for AI audio.

## License

The plugin files in this repository are MIT licensed. Benaiah's hosted service, trademarks and customer data are not licensed by this repository.
