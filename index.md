---
layout: default
---

# Borlandux LLC

Borlandux is the single-member ML & statistics consultancy of
[Gonzalo Barrera Borla](https://capitantoto.github.io). I build turnkey data
science and machine learning solutions: embedded IC/staff engagements or
scoped, fixed-deliverable projects. I work remote from Buenos Aires (UTC-3),
with full US East Coast overlap.

## Selected engagements

- **Sitch** (matchmaking startup, first data hire): helped build an
  LLM-powered matchmaking chatbot, then cut LLM costs by >95% — replacing
  LLM-only affinity scoring with chat-NLP extraction, GBT match-probability
  models and greedy b-matching — from >10K USD/mo in OpenAI fees to a few
  bare-metal VMs, holding human-curated match quality while scaling from
  3K to 30K MAU.
- **Move 37** (pari-mutuel horse-racing syndicate): led quantitative R&D
  (team of 4); upgraded bet sizing from single-wager fractional Kelly to
  joint Kelly over correlated wagers. Volume scaled over 2× at stable
  margins while adding trifectas and superfectas.
- **Muun Wallet** (self-custodial BTC & Lightning wallet): real-time
  incongruity detection plus ad-hoc on-chain and Lightning contracts drove
  ~2 BTC/mo of micro-fraud to near zero — over 200K USD/mo then.
- **US cold-storage warehousing provider**: order fulfillment-time
  prediction service integrated into their ERP, showcased by the client CEO
  at their ERP vendor's annual conference.
- **Unilever USA**: 1-year vendor-decoupling roadmap for their freight
  invoice audit operation — about USD 1B/yr over 500K+ invoices.

## Writing

{% for post in site.posts %}
- [{{ post.title }}]({{ post.url }}) — {{ post.date | date: "%Y-%m-%d" }}
{% endfor %}

## Contact

- [gonzalobb@gmail.com](mailto:gonzalobb@gmail.com)
- [capitantoto.github.io](https://capitantoto.github.io)
- [LinkedIn](https://www.linkedin.com/in/gonzabb/)
