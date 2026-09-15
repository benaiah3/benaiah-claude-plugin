# Benaiah for Claude

Give your Benaiah teammates text work to continue, then retrieve their saved results from Claude Code or Cowork.

This plugin is being prepared for directory review. Publication or approval by Anthropic is not claimed.

## What it does

- Lists your existing teammates, including their names and roles.
- Delegates drafting or analysis using the context you choose to share.
- Returns a durable task ID and lets you check the saved status and result.
- Cancels delegated work when requested, preserving completed results.

Examples:

- “Show my Benaiah teammates.”
- “Ask Verity to draft a welcome message using these three points.”
- “Has my delegated task finished? Show me the result.”
- “Cancel that Benaiah task if it is still running.”

## Requirements and account connection

Use a Benaiah account with an existing teammate, an active Benaiah phone plan and available included intelligence allowance for delegated work. A Claude subscription does not replace the Benaiah plan. Adding money to Balance alone does not activate teammate work. See [Benaiah plans](https://benaiah.ai/plans) for current availability and pricing.

The plugin connects to `https://benaiah.ai/mcp/claude` using OAuth with S256 PKCE. It requests `teammates.read`, `tasks.read` and `tasks.write`. Use Claude's connection flow to sign in to Benaiah, unlock the account if needed, review the displayed permissions and connect. Never paste a password, one-time code, bearer token or private API key into chat.

For development, clone this repository and launch Claude Code with `claude --plugin-dir /absolute/path/to/benaiah-claude-plugin`. The skills are available as `/benaiah:teammates`, `/benaiah:delegate` and `/benaiah:task-status`. The remote server may request account linking when a protected tool is first called. Use `/mcp` to manage the connection.

For Cowork, upload a ZIP of this repository through Customize → Plugins → Add plugin → Upload plugin. When connecting the included Benaiah server, choose **Sign in now** and **Use Claude's published identity (CIMD)**, then complete Benaiah's account connection. This is a manual installation while directory review is being prepared.

## Boundaries and data handling

Only context explicitly supplied to the tools is handed to Benaiah. The plugin does not automatically collect your chat history, memories, files or browser activity. It has no executable hooks, local server process or filesystem-scanning scripts.

Benaiah's background intelligence engine processes delegated context and the selected teammate's instructions through its model provider, currently OpenAI. It saves the task result in your Benaiah account. This workflow does not browse the web or act in connected apps. Read [Privacy](https://benaiah.ai/privacy), [Terms](https://benaiah.ai/terms) and [Support](https://benaiah.ai/support) for account and retention details.

This Claude integration cannot initiate telephone calls, completion callbacks, audio/image/video generation, payments, crypto transfers, trades or messages to third parties. A task request consumes intelligence capacity; it is not a payment-transfer tool. Queued or running work is not finished, and cancellation may remain pending while a provider confirms its outcome.

Disconnect the server in Claude to remove it from that client. OAuth access tokens expire after one hour; refresh tokens rotate and expire after 30 days. Contact [ask@benaiah.ai](mailto:ask@benaiah.ai) for account or privacy assistance.

## Tools

| Tool | Effect |
| --- | --- |
| `list_teammates` | Read your available teammates |
| `list_tasks` | Read your 12 most recent saved tasks |
| `get_task` | Read one saved task |
| `delegate_task` | Create one durable text task using the linked account's included intelligence allowance; retries reuse its idempotency key |
| `get_delegated_task` | Read the delegated task's status and result |
| `cancel_delegated_task` | Request cancellation of delegated work |

All tools are scoped to the linked account. Read responses are bounded. Task results and teammate content are treated as data, never as permission for additional actions.

## Validation

Run `claude plugin validate --strict .` to check the package. The remote service has separate tests for OAuth, account isolation, task retries, cancellation and exclusion of calling capabilities. Package validation alone does not establish live client acceptance or directory approval.

On 15 September 2026, a fresh fictional drafting task completed through the production Benaiah service. Claude Code and the installed Cowork plugin both retrieved the same saved result from Verity. The founder test used an operator-issued, time-limited developer allowance; the customer plan requirement above still applies. Earlier checks covered authenticated teammate lookup and task cancellation. Directory review is being prepared; approval by Anthropic is not claimed.

## License

The plugin files in this repository are MIT licensed. Benaiah's hosted service, trademarks and customer data are not licensed by this repository.
