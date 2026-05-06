# DRO-CA: Distributionally Robust Neural Mechanism for Strategy-Proof Combinatorial Auctions

This repository contains the LaTeX source, figures, tables, bibliography files, and NeurIPS submission template for writing a full research paper entitled:

**DRO-CA: Distributionally Robust Neural Mechanism for Strategy-Proof Combinatorial Auctions**

The goal of this project is to produce a complete, rigorous, publication-ready NeurIPS-style paper. The paper proposes **DRO-CA**, a distributionally robust neural mechanism design framework for strategy-proof combinatorial auctions under valuation distribution shift.

## Research Motivation

Combinatorial auctions allow bidders to express preferences over bundles of items. They are essential in settings such as spectrum auctions, cloud-resource allocation, procurement, advertising packages, and logistics markets. However, the valuation space grows exponentially with the number of items, and practical auction-design methods often rely on learned or parameterized mechanisms.

Recent neural auction-design methods can optimize revenue on a known training valuation distribution, but they commonly assume that the training and deployment distributions match. This assumption is fragile. In real markets, bidder valuations may shift due to changes in demand, complementarity structure, item scale, market environment, or bidding complexity.

This paper studies the following question:

> Can we design strategy-proof neural combinatorial auction mechanisms that remain robust under valuation distribution shift?

DRO-CA addresses this question by incorporating distributionally robust optimization into offline menu-based neural mechanism design.

## Core Idea

DRO-CA learns a bid-independent randomized bundle menu by optimizing revenue not only under the empirical training valuation distribution, but also under worst-case valuation distributions inside an ambiguity set.

The central robust objective can be written conceptually as:

\max_{\mathcal{B}}
\min_{Q \in \mathcal{U}(\widehat{P})}
\mathbb{E}_{v \sim Q}
\left[
R_{\mathcal{B}}(v)
\right],

where:

\widehat{P} is the empirical training valuation distribution,
\mathcal{U}(\widehat{P}) is an ambiguity set around the empirical distribution,
\mathcal{B} is a bid-independent menu of randomized bundle allocations and prices,
R_{\mathcal{B}}(v) is the revenue obtained from valuation v.

Because the deployed mechanism remains a bid-independent menu mechanism and bidders select utility-maximizing menu entries, the robust objective changes the offline optimization target but does not destroy the strategy-proof menu-selection structure.

Main Contributions

The paper should emphasize the following contributions:

Distributionally robust neural combinatorial auction design
We introduce DRO-CA, a framework that learns strategy-proof neural combinatorial auction mechanisms under valuation distribution shift by optimizing against ambiguity sets around the empirical valuation distribution.
CATS-based distribution shift benchmark
We construct controlled train-test shifts based on the Combinatorial Auction Test Suite (CATS), including value-distribution shift, environment shift, XOR-complexity shift, item-scale shift, complementarity shift, and mixed shift.
Robust revenue and tail-risk improvements
DRO-CA improves out-of-distribution revenue, worst-case revenue, CVaR revenue, and revenue retention compared with ERM neural auctions, adversarial training, CVaR training, and classical menu baselines.
Preservation of strategy-proof structure
DRO-CA modifies only the offline menu-optimization objective. The deployed mechanism remains a bid-independent menu mechanism, preserving dominant-strategy incentive compatibility under the menu model.
Ablation and diagnostics
We analyze the contribution of ambiguity sets, adversarial valuation sampling, CVaR protection, radius scheduling, and different ambiguity-set families, while also reporting incentive, feasibility, runtime, and reproducibility diagnostics.
Repository Structure

The repository should contain a structure similar to:

.
├── ALL_Fig/
│   ├── fig2_id_ood_tradeoff.pdf
│   ├── fig3_shift_type_robustness.pdf
│   ├── fig4_radius_sensitivity.pdf
│   ├── figA2_revenue_tail_cdf.pdf
│   ├── figA3_radius_by_shift_type.pdf
│   └── figA4_menu_heatmap.pdf
├── ALL_Tables.tex
├── bundleflow.pdf
├── checklist.tex
├── custom.bib
├── neurips_2026.sty
├── neurips_2026.tex
├── nips.bst
└── README.md

The final paper uses six figures and six tables.

Final Figure List

Use exactly the following six figures.

Figure 1: In-Distribution and Out-of-Distribution Revenue Trade-off

File:

ALL_Fig/fig2_id_ood_tradeoff.pdf

Purpose:

This is the main visual result. It shows the ID-OOD revenue Pareto trade-off. DRO-CA variants should lie on a better frontier than ERM, adversarial training, CVaR training, and classical baselines.

Suggested caption:

In-distribution and out-of-distribution revenue trade-off. Each point represents a mechanism evaluated under the same CATS shift benchmark. DRO-CA variants achieve substantially higher out-of-distribution revenue while retaining competitive in-distribution revenue, yielding a stronger Pareto frontier than ERM and non-robust baselines.

Figure 2: Robustness across Distribution Shift Types

File:

ALL_Fig/fig3_shift_type_robustness.pdf

Purpose:

This figure reports revenue retention across representative distribution shifts, including Uniform-to-Normal, Regions-to-Arbitrary, XOR-complexity shift, and item-scale shift.

Suggested caption:

Robustness across distribution shift types. DRO-CA variants consistently improve revenue retention under value-distribution, environment, XOR-complexity, and item-scale shifts, indicating that the gains are not tied to a single shift pattern.

Figure 3: Sensitivity to Ambiguity Radius

File:

ALL_Fig/fig4_radius_sensitivity.pdf

Purpose:

This figure shows how ID revenue, OOD revenue, worst-case revenue, and DSIC regret change as the ambiguity radius increases.

Suggested caption:

Sensitivity to ambiguity radius. Moderate ambiguity radii improve out-of-distribution and worst-case revenue, while overly large radii become conservative. DSIC regret remains low because the deployed mechanism retains the bid-independent menu-selection structure.

Figure 4: Revenue Distribution and Tail CDF

File:

ALL_Fig/figA2_revenue_tail_cdf.pdf

Purpose:

This figure supports the distributional robustness claim by showing revenue distribution and lower-tail behavior under shift. It can be placed in the main paper if space allows, or in the appendix.

Suggested caption:

Revenue distribution and lower-tail CDF under distribution shift. DRO-CA shifts revenue mass toward higher values and improves lower-tail behavior, reducing the probability of catastrophic low-revenue outcomes compared with ERM and CVaR baselines.

Figure 5: Radius Sensitivity by Shift Type

File:

ALL_Fig/figA3_radius_by_shift_type.pdf

Purpose:

This appendix figure expands radius sensitivity across value, environment, complexity, scale, complementarity, and mixed shifts.

Suggested caption:

Radius sensitivity by shift type. Across shift families, intermediate ambiguity radii generally yield the strongest OOD retention, while excessively large radii can become conservative.

Figure 6: Robust Menu Structure Heatmap

File:

ALL_Fig/figA4_menu_heatmap.pdf

Purpose:

This figure compares learned menu structures under ERM and DRO-CA. It should support the interpretation that DRO-CA learns more diversified, robust bundle coverage.

Suggested caption:

Robust menu structure heatmap. Rows represent menu entries and columns represent items. Compared with ERM, DRO-CA learns more diversified menu coverage, reducing sparsity and improving allocation robustness under shifted valuation distributions.

Important Note on Removed Figure

A previous planning version included a figure named fig1_cats_distribution_shift.pdf or an overview/shift-construction figure. The current project intentionally keeps only the six figure files listed above. Do not refer to missing figures. The paper should renumber the existing figures naturally.

Final Table List

Use exactly six tables. The LaTeX for all tables is stored in:

ALL_Tables.tex

The six tables are:

Table 1: CATS Distribution Shift Benchmark
Defines the benchmark settings, including shift IDs, train/test environments, valuation distributions, item counts, XOR atoms, and shift type.
Table 2: Main Results under Distribution Shift
Reports ID revenue, OOD revenue, worst-case revenue, CVaR@20% revenue, revenue retention, and incentive regret.
Table 3: OOD Revenue by Shift Type
Reports OOD revenue separately for value, environment, complexity, scale, complementarity, and mixed shifts.
Table 4: Ablation and Ambiguity Set Comparison
Combines component ablations and ambiguity-set comparison, including Wasserstein, KL, chi-square, total variation, adversarial neighborhood, and mixture DRO variants.
Table 5: Incentive, Feasibility, and Runtime Diagnostics
Reports mean regret, max regret, IR violation, feasibility violation, training time, and inference time.
Table 6: Hyperparameters and Reproducibility Details
Reports all major CATS generation, auction learner, DRO objective, Wasserstein, f-divergence, adversarial sampler, CVaR, and evaluation settings.
Suggested Paper Structure

The final paper should follow this NeurIPS-style structure:

\begin{abstract}
...
\end{abstract}

\section{Introduction}

\section{Related Work}
\subsection{Combinatorial Auctions and XOR Valuations}
\subsection{Automated and Neural Mechanism Design}
\subsection{Distributionally Robust Optimization}
\subsection{Robustness and Generalization in Auction Design}

\section{Problem Formulation}
\subsection{Combinatorial Auction Setting}
\subsection{Menu-Based Strategy-Proof Mechanisms}
\subsection{Distribution Shift in Valuation Distributions}
\subsection{Robust Revenue Criteria}

\section{DRO-CA}
\subsection{Overview}
\subsection{Empirical Valuation Distribution and Shift Model}
\subsection{Ambiguity Sets}
\subsection{Distributionally Robust Menu Objective}
\subsection{Adversarial Valuation Sampling}
\subsection{Training and Deployment}

\section{Theoretical Analysis}
\subsection{Dominant-Strategy Incentive Compatibility}
\subsection{Individual Rationality}
\subsection{Robust Revenue Lower Bound}
\subsection{Relation between Ambiguity Radius and Conservatism}

\section{CATS Distribution Shift Benchmark}
\subsection{Benchmark Construction}
\subsection{Shift Types}
\subsection{Evaluation Metrics}

\section{Experiments}
\subsection{Experimental Setup}
\subsection{Main Results under Distribution Shift}
\subsection{Revenue by Shift Type}
\subsection{Ambiguity Radius Sensitivity}
\subsection{Ablation and Ambiguity Set Comparison}
\subsection{Incentive, Feasibility, and Runtime Diagnostics}

\section{Limitations and Broader Impacts}

\section{Conclusion}

\appendix

\section{Additional Experimental Details}
\section{Additional Robustness Results}
\section{Menu Structure Analysis}
\section{Additional Theoretical Discussion}
\section{NeurIPS Checklist}
Recommended Figure Placement

Use this mapping when writing the paper:

Place fig2_id_ood_tradeoff.pdf as Figure 1 in the main results section.
Place fig3_shift_type_robustness.pdf as Figure 2 in the shift-wise robustness section.
Place fig4_radius_sensitivity.pdf as Figure 3 in the ambiguity radius sensitivity section.
Place figA2_revenue_tail_cdf.pdf as Figure 4 either in the main paper or appendix.
Place figA3_radius_by_shift_type.pdf as Appendix Figure A1 or Figure 5 depending on whether the template keeps appendix figures separately.
Place figA4_menu_heatmap.pdf as Appendix Figure A2 or Figure 6.

If the main paper has limited space, put the last three figures in the appendix. If space is available, keep the revenue tail figure in the main paper because it strongly supports the distributional robustness claim.

Recommended Table Placement
Table 1 should appear in the benchmark section.
Table 2 should appear in the main results section.
Table 3 should appear in the shift-wise results section.
Table 4 should appear in the ablation section.
Table 5 should appear in the diagnostics section.
Table 6 should appear in the appendix or reproducibility section.
Required Mathematical Content

Define the following notation:

Item set: M = {1, ..., m}
Bundle: S \subseteq M
Valuation: v: 2^M \to \mathbb{R}_{\ge 0}
XOR valuation representation: z = {(S_j, a_j)}_{j=1}^{q}
Empirical training valuation distribution: \widehat{P}
Deployment/test valuation distribution: P_{\mathrm{test}}
Ambiguity set: \mathcal{U}_{\rho}(\widehat{P})
Menu: \mathcal{B} = {(\alpha_k, p_k)}_{k=0}^{K}
Utility: u_v(\alpha_k,p_k) = v(\alpha_k) - p_k
Bidder choice rule: k^*(v)=\arg\max_k u_v(\alpha_k,p_k)
Revenue: R_{\mathcal{B}}(v)=p_{k^*(v)}
ERM objective
DRO objective
CVaR objective
Worst-case revenue
Revenue retention
Incentive regret
Required Theoretical Statements

The paper should contain rigorous but concise theoretical statements.

Proposition 1: DSIC of Bid-Independent Menu Selection

State that if the deployed menu is independent of the bidder's report and the bidder receives the utility-maximizing menu entry, then truthful utility maximization is a dominant strategy under the menu model.

Proposition 2: Individual Rationality

If the menu contains a null entry with zero allocation and zero payment, then the bidder can always guarantee non-negative utility by selecting the null entry.

Proposition 3: DRO Revenue Lower Bound

If the true test valuation distribution lies within the ambiguity set, then the DRO objective lower-bounds test revenue:

P_{\mathrm{test}} \in \mathcal{U}_{\rho}(\widehat{P})
\quad \Rightarrow \quad
\mathbb{E}_{v\sim P_{\mathrm{test}}}
[R_{\mathcal{B}}(v)]
\ge
\inf_{Q\in \mathcal{U}_{\rho}(\widehat{P})}
\mathbb{E}_{v\sim Q}
[R_{\mathcal{B}}(v)].
Proposition 4: Radius-Conservatism Trade-off

Explain formally or semi-formally that increasing the ambiguity radius enlarges the uncertainty set, making the robust objective more conservative. This can improve OOD revenue up to a point but may reduce ID revenue when the radius is too large.

Baselines to Discuss

The paper should define and discuss:

Grand Bundle
Menu+
Menu-
Product-Menu Network
ERM Neural Auction
Adversarial Training
CVaR Auction
DRO-CA-Wasserstein
DRO-CA-f-divergence
DRO-CA-Adversarial
Mixture DRO
Oracle Test Distribution

The oracle test-distribution mechanism should be explicitly described as an upper-reference baseline that has access to the test valuation distribution and is not available in deployment.

Metrics to Define

The paper must define:

ID revenue
OOD revenue
Worst-case revenue
CVaR@20% revenue
Revenue retention
Revenue drop
Social welfare if used
Mean regret
Max regret
IR violation
Feasibility violation
Training time
Inference time
Writing Style

Use a rigorous NeurIPS/ICML writing style:

Clear definitions before equations.
Formal but readable paragraphs.
Avoid exaggerated claims.
Make assumptions explicit.
Distinguish empirical robustness from formal worst-case guarantees.
State that the robust guarantee is conditional on the test distribution lying in the ambiguity set.
Do not claim that DRO-CA solves all distribution shifts.
Use careful wording for strategy-proofness: the robust objective changes training, but the deployed menu-selection rule preserves the strategy-proof structure.
Reference Paper

If bundleflow.pdf is present, use it only for background and positioning. Do not write this paper as a minor extension of BundleFlow. The current paper should be framed as a new distributionally robust neural mechanism design framework.

Useful background from the reference paper:

Combinatorial auctions are difficult because bundle spaces grow exponentially.
CATS is a standard benchmark for combinatorial auctions.
CATS-Regions and CATS-Arbitrary are challenging environments.
CATS valuations use XOR bidding language.
Menu-based mechanisms can guarantee strategy-proofness when the menu is bid-independent and bidders choose utility-maximizing entries.
Compilation

A typical compilation command is:

pdflatex neurips_2026.tex
bibtex neurips_2026
pdflatex neurips_2026.tex
pdflatex neurips_2026.tex

If using Overleaf, compile neurips_2026.tex.

Notes for Codex

Codex should:

Inspect the repository tree.
Open neurips_2026.tex, ALL_Tables.tex, custom.bib, and checklist.tex.
Complete neurips_2026.tex into a full paper.
Insert all six figures with correct paths.
Insert or input all six tables.
Add missing BibTeX entries to custom.bib.
Ensure all labels and references compile.
Ensure the NeurIPS checklist is included if required.
Ensure the final output is a coherent full paper, not only a skeleton.
