# n8n-workflows

Automation systems I've built in n8n, with Claude for the judgement calls and Clay for enrichment. Each folder has the workflow screenshot and a node-by-node breakdown.

| Workflow | Stack | What it does |
|---|---|---|
| [**reply-sorter-router**](workflows/reply-sorter-router) | n8n · Gmail · Claude · Google Sheets · Slack | Matches every reply to its prospect, classifies it, drafts responses to interested leads, and schedules out-of-office follow-ups |
| [**meeting-brief-pipeline**](workflows/meeting-brief-pipeline) | n8n · Calendly · Clay · Claude · Slack | A Calendly booking turns into an enriched, Claude-written pre-call brief in your inbox and on Slack |
| [**gift-order-automation**](workflows/gift-order-automation) | n8n · Clay · Claude · Paystack · Google Sheets · Slack | A whole gift business in 3 workflows: form, enrichment, AI gift picks, Slack approval, proposal, payment, fulfilment |

<p align="center">
  <img src="docs/img/reply-sorter-router.png" width="100%" alt="Reply Sorter & Router">
</p>

## Patterns used throughout

- **Structured output on every classification.** Claude returns schema-validated JSON, so `IF` and `Switch` nodes branch on fields instead of parsing free text.
- **AI drafts, humans send.** Replies are saved as Gmail drafts, and gift picks wait for a Slack approval. The repetitive work is automated and people make the final call.
- **Async hand-offs instead of waiting.** n8n sends records to Clay and moves on, and Clay calls back with a webhook when enrichment is done.
- **Idempotent by design.** "Mark as read", "mark drafted" and "skip already paid" mean a retry or duplicate event never does the work twice.
- **One sheet as the source of truth.** Every step writes its status back, so you can always see where a lead or order is.

## Related

- [lead-qualification-pipeline](https://github.com/zinkwonri-kayinu/lead-qualification-pipeline): the gate between enrichment and sequencing
- [multichannel-outbound-orchestrator](https://github.com/zinkwonri-kayinu/multichannel-outbound-orchestrator): pushes qualified leads to Instantly + HeyReach

## License

MIT
