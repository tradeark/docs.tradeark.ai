# AI Risk Firewall

TradeArk includes a local AI risk firewall for OpenClaw, Codex, Claude Code, and similar local agent workflows. Its purpose is simple: let AI use the local trading surface without giving the AI unrestricted raw exchange credentials.

![TradeArk AI risk control page](../assets/ui/en/ai-firewall-overview.png)

## What the firewall is protecting

The firewall sits between an AI client and exchange write actions such as:

- placing an order
- cancelling an order
- cancelling all open orders
- closing positions
- changing leverage or margin mode

Normal reads such as balances, positions, history, symbols, and market data can stay on the same local machine as before. The firewall matters when the workflow moves from "observe" to "write".

## The two layers

TradeArk uses two layers instead of one:

### 1. Pre-trade policy layer

Before a write request is forwarded to the exchange, TradeArk can evaluate:

- which saved accounts the AI client is allowed to touch
- which routes are allowed
- which symbols or market types are allowed
- leverage ceilings
- max quantity or max notional
- daily or rate limits

If the request is out of scope, it is blocked locally before the exchange sees it.

### 2. Post-trade watchdog layer

After exposure exists, a second local layer can keep watching balances, open orders, and positions. Depending on your configuration, it can:

- raise an alert
- cancel open orders
- flatten swap exposure
- freeze the AI client
- freeze the affected account

This means the firewall is not only about blocking bad requests up front. It can also react when a previously accepted workflow starts drifting into unsafe territory.

## Typical setup flow

If you want to connect an external local AI tool, the safest rollout order is:

1. Create a named AI client in the local Web UI.
2. Bind it only to the saved accounts that workflow should use.
3. Keep route scope narrow at first.
4. Set leverage, quantity, notional, and frequency limits before enabling writes.
5. Generate the ready-to-paste prompt or client instructions from the UI.
6. Start in read-only behavior or testnet behavior first.
7. Enable real write routes only after the full path is validated.

## What operators should verify

Before trusting an AI workflow with live writes, confirm:

- the target account is the correct one
- the market type and symbol scope are correct
- the exchange permissions match the intended workflow
- manual orders already succeed in the same environment
- TP / SL behavior has been verified in that exact exchange setup
- watchdog actions are understood before the first live run

## Important boundaries

The firewall improves control, but it does not replace operator judgment.

- It does not turn a bad strategy into a good one.
- It does not fix an exchange account with overly broad permissions.
- It does not remove the need for testnet validation.
- It should not be treated as permission to skip small-size rollout.

## Practical guidance

- Prefer `account_id` and saved local accounts instead of sending raw keys in every request.
- Use one named AI client per workflow, bot, or operator instead of sharing one token across everything.
- Rotate or revoke the client quickly when a workflow changes ownership or purpose.
- If a workflow only needs analysis, keep it read-only and do not expose write routes at all.

## Where to continue

- For model provider setup, continue with [AI Model Center](ai-model-center.md).
- For chart-side AI features, continue with [Bottom-Right AI Analysis](ai-chart-analysis.md).
- For scripted integration details and route behavior, continue with [API Appendix (Advanced)](../reference/api.md).
