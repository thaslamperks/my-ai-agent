# Paid Domain Research (optional skill)

Ask the agent to research a business website and it uses this skill first. It looks up real search data for that domain, works out what the business appears to offer, finds the keywords it already ranks for, spots the sites competing with it in Google, and saves all of it on your computer for later conversations.

Best for: deciding what to write next, seeing where you already show up in search, and finding out who is beating you to the same searches.

This skill costs money per run, because it uses the DataForSEO service. The free `domain-research` skill reads only the home page and costs nothing. See [`../domain-research/README.md`](../domain-research/README.md).

## Before you start

You need a DataForSEO account and a small amount of credit on it. Set the credential up privately in n8n, exactly as described in [`docs/PAID_DOMAIN_RESEARCH.md`](../../docs/PAID_DOMAIN_RESEARCH.md). Never paste your API login or password into the chat, a file in this project, or a screenshot.

You also need the Anthropic credential you already created for workflow `00`. This skill reuses it.

## Turn it on

1. Open `skills/enabled.txt` and add this line at the end:

   ```text
   paid-domain-research
   ```

2. Save the file. Do not change any other line in it.
3. Make sure the local app is running, then sync:
   - macOS: double-click `sync-skills.command`
   - Windows: double-click `sync-skills-windows.cmd`
4. Wait for **Enabled skills synced successfully**.
5. Open the chat and select **New conversation**.

## Try it

```text
Please research yourbusiness.com.
```

That is the whole instruction. The agent will not ask whether you own the domain, and it will not ask you to approve the cost a second time: asking for the research is the approval. It runs one standard search, aimed at Australia and English, with a spending ceiling of about US$0.20.

If you want a cheaper or deeper look, say so in the request:

- `Do a refresh check on yourbusiness.com` — about US$0.10
- `Do deep research on yourbusiness.com` — about US$0.50

Then wait. One run takes up to a minute. Do not send the message again; the agent never repeats a paid search on its own.

## What you get back

- What the business does
- The best keyword opportunities, with a short reason for each
- Competitors worth watching, split into real business rivals and sites competing for the same Google results
- Three practical next steps
- A short note about the evidence when something is missing or uncertain
- The actual cost of the run, in one closing line

## When the paid data does not arrive

If DataForSEO is unavailable or the search returns nothing useful, the agent falls back to the free `domain-research` skill and tells you plainly that the result comes from the public website instead. It never retries the paid search by itself, and it never presents a failed request as "no results found".

A partial result is kept and reported as partial. A failed attempt never overwrites research that succeeded earlier.

## Costs and control

The spending ceilings above are limits this project applies, based on DataForSEO's published prices. They are not a promise from the provider. Set an account budget in your DataForSEO dashboard as the final billing control. Full detail, including how each stage reserves its share of the ceiling, is in [`docs/PAID_DOMAIN_RESEARCH.md`](../../docs/PAID_DOMAIN_RESEARCH.md).

## Where your research is stored

On your computer, in the chat app's local database, alongside your saved conversations. Nothing is uploaded anywhere except the searches sent to DataForSEO, the request to read the public page, and the analysis request to Claude.

## Turn it off

Delete the `paid-domain-research` line from `skills/enabled.txt` and sync again. The free `domain-research` skill keeps working on its own, and research already saved stays saved.
