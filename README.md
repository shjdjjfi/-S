# NL-Auction: The Strategy-Proof Combinatorial Auction Framework from Natural-Language Preferences

This repository contains the LaTeX source, figures, tables, bibliography, and reference material for writing a NeurIPS-style research paper entitled:

**NL-Auction: The Strategy-Proof Combinatorial Auction Framework from Natural-Language Preferences**

The goal of this project is to write a complete, rigorous, and publication-ready NeurIPS-style paper. The paper proposes **NL-Auction**, a new framework that connects natural-language preference elicitation with strategy-proof combinatorial auction design.

## Project Motivation

Combinatorial auctions allow bidders to express preferences over bundles of items, which is essential when items exhibit complementarities. However, most existing combinatorial auction design methods assume that bidder valuations are already provided in structured formats such as XOR bidding language. In practical markets, bidders often express preferences in natural language, and fully specifying structured bundle-value functions is costly, unrealistic, or cognitively difficult.

This paper studies the following question:

> Can we design a strategy-proof combinatorial auction mechanism directly from natural-language bidder preferences?

NL-Auction addresses this question by converting natural-language bidder descriptions into uncertainty-aware combinatorial valuation posteriors and then using these posteriors for strategy-proof auction design.

## Core Contributions

The paper should emphasize the following contributions:

1. **Natural-language combinatorial preference elicitation**  
   We introduce a framework that maps free-form bidder preference descriptions into uncertainty-aware distributions over combinatorial valuations.

2. **Strategy-proof auction design from elicited valuation posteriors**  
   NL-Auction propagates elicitation uncertainty into the auction-design objective, rather than first reconstructing a single point estimate of the valuation function.

3. **NL-CATS benchmark**  
   We construct NL-CATS by converting structured CATS XOR valuations into natural-language bidder descriptions with multiple linguistic styles and ambiguity levels.

4. **Robustness under language noise**  
   We evaluate how auction revenue, welfare, and incentive regret change under clean, paraphrased, ambiguous, noisy, and incomplete language inputs.

5. **Mechanism-aware elicitation insight**  
   The paper should highlight that perfect valuation reconstruction is not necessary for strong auction performance. Mechanism-aware elicitation can yield better revenue than point reconstruction even at similar reconstruction error.

## Repository Structure

The repository currently contains:

```text
.
├── ALL_Fig/
│   ├── fig1_nl_auction_demo.pdf
│   ├── fig3_language_noise.pdf
│   ├── fig4_valuation_error_vs_revenue.pdf
│   └── fig5_scalability.pdf
├── ALL_Tables.tex
├── bundleflow.pdf
├── checklist.tex
├── custom.bib
├── neurips_2026.sty
├── neurips_2026.tex
├── nips.bst
└── README.md
