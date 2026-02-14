# My First Draft

## Source Information

**Date written:** February 14, 2026

**Context:** This is a draft of Introduction and Literature Review sections from my research paper on Online Convex Optimization with time-varying constraints. This will be used for the COMP6020 course assignment (Task 3.2 - Writing Sample Collection).

**Status:** Complete draft - includes full Introduction and Literature Review (Related Work) sections

---

## Introduction

**[Move 1 – Establishing a Territory]**

Online Convex Optimization (OCO) is a vital framework for sequential decision-making under uncertainty \cite{Book:S.Shwartz'12}\nocite{Book:E.Hazan'16}-\cite{Book:F.Orabona'19}. The standard OCO models a sequential game between a learner and an adversary over time. At each time, the learner first selects a decision from a bounded convex feasible set. The adversary then reveals a convex loss function, and the learner incurs the corresponding loss. Faced with unknown loss functions, the learner cannot achieve the optimal performance. Instead, the learner aims to minimize the \textit{regret}, which quantifies the cumulative performance gap between its online decisions and the best fixed decision in hindsight. The seminal OCO work~\cite{OCO:M.Zinkevich-ICML'03} achieved $\mathcal{O}(\sqrt{T})$ regret for a sequence of $T$ arbitrary convex loss functions (with bounded gradients). The regret was improved to $\mathcal{O}(\log{T})$ for strongly convex loss functions \cite{OCO:E.Hazan-ML'07}.

The standard OCO requires constraints to be strictly satisfied at each time, which often involves computationally expensive projection operations onto the feasible set \cite{OCO:M.Zinkevich-ICML'03}\nocite{OCO:E.Hazan-ML'07}\nocite{DOCO:E.C.Hall-JTSP'15}\nocite{DOCO:L.Zhang-NIPS'18}\nocite{DOCO:N.Eshraghi-ICML'20}-\cite{DOCO:L.Zhang-JMLR'24}. Furthermore, many practical networking applications \cite{Application:N.Liakopoulos-ICML'19}\nocite{Application:M.Shi-TON'21}\nocite{Application:W.-K.Hsu-OR'22}-{\cite{Application:J.Wang-TON'25}} only require constraints to be satisfied cumulatively over time. These motivate constrained OCO (COCO) {\cite{SCOCO-Fix:M.Mahdavi-MLR'12}\nocite{SOCO-Fix:R.Jenatton-ICML'16}\nocite{SOCO-Fix:H.Yu-JMLR'20}\nocite{HOCO-Fix:J.Yuan-NeurIPS'18}\nocite{HOCO-Fix:X.Yi-ICML'21}\nocite{HOCO-Varying:H.Guo-NeurIPS'22}\nocite{SOCO-Varying:X.Cao-TAC'19}\nocite{SOCO-Varying:M.J.Neely-ArXiv'17}\nocite{HOCO-Varying:A.Sinha-NeurIPS'24}\nocite{HOCO-Varying:Lekeufack-ArXiv'24}\nocite{SOCO-Varying:T.Chen-TSP'17}\nocite{SOCO-Varying:Q.Liu-SIGMETRICS'22}\nocite{SOCO-Varying:J.Wang-TON'23}-\cite{HOCO-Varying:J.Wang-AAAI'25}}, where some constraints in the feasible set are relaxed to long-term constraints. In COCO, the learner aims to simultaneously minimize the regret and the cumulative \textit{constraint violation} over time. 

**[Move 2 – Identifying a Niche]**

Early COCO works focused on \textit{known time-invariant} constraints \cite{SCOCO-Fix:M.Mahdavi-MLR'12}\nocite{SOCO-Fix:R.Jenatton-ICML'16}\nocite{SOCO-Fix:H.Yu-JMLR'20}\nocite{HOCO-Fix:J.Yuan-NeurIPS'18}\nocite{HOCO-Fix:X.Yi-ICML'21}-\cite{HOCO-Varying:H.Guo-NeurIPS'22}, proposing two constraint violation metrics: \textit{soft} violation allowing compensated violations~\cite{SCOCO-Fix:M.Mahdavi-MLR'12} and \textit{hard} violation prohibiting any compensated violation over time~\cite{HOCO-Fix:J.Yuan-NeurIPS'18}. The hard violation has attracted more attention since a bound on hard violation \cite{HOCO-Fix:J.Yuan-NeurIPS'18}\nocite{HOCO-Fix:X.Yi-ICML'21}-\cite{HOCO-Varying:H.Guo-NeurIPS'22} readily implies a bound on soft violation \cite{SCOCO-Fix:M.Mahdavi-MLR'12}\nocite{SOCO-Fix:R.Jenatton-ICML'16}-\cite{SOCO-Fix:H.Yu-JMLR'20}. For \textit{fixed} constraints, state-of-the-art COCO algorithms achieved both $\mathcal{O}(1)$ soft \cite{SOCO-Fix:H.Yu-JMLR'20} (requiring Slater's condition) and hard violation \cite{HOCO-Varying:H.Guo-NeurIPS'22}. 

Recent COCO works studied \textit{unknown time-varying} constraints \cite{HOCO-Varying:H.Guo-NeurIPS'22}\nocite{SOCO-Varying:X.Cao-TAC'19}\nocite{SOCO-Varying:M.J.Neely-ArXiv'17}\nocite{HOCO-Varying:A.Sinha-NeurIPS'24}-{\cite{HOCO-Varying:Lekeufack-ArXiv'24}}, where both the loss and constraint functions are revealed only after the learner selects its decision. This adversarial setting inevitably incurs constraint violations. For \textit{arbitrary} convex constraints (with bounded gradients and/or values), state-of-the-art COCO algorithms achieved $\mathcal{O}(\sqrt{T})$ soft violation~\cite{SOCO-Varying:M.J.Neely-ArXiv'17} (requiring Slater's condition) and $\mathcal{O}(\sqrt{T}\log{T})$ hard violation~\cite{HOCO-Varying:A.Sinha-NeurIPS'24}. However, compared with the best-known $\mathcal{O}(1)$ violations for fixed constraints in the time-invariant COCO world, the best-known violations for arbitrary constraints increase significantly to $\Omega(\sqrt{T})$ in the time-varying COCO world.

To bridge the above two COCO worlds, some works quantify the cumulative constraint variation over time, enabling a \textit{unified} constraint violation analysis for both time-invariant and time-varying COCO \cite{SOCO-Varying:T.Chen-TSP'17}\nocite{SOCO-Varying:Q.Liu-SIGMETRICS'22}\nocite{SOCO-Varying:J.Wang-TON'23}-{\cite{HOCO-Varying:J.Wang-AAAI'25}}. Along this direction, the state-of-the-art algorithm \cite{HOCO-Varying:J.Wang-AAAI'25} achieved $\mathcal{O}(T^v)$ hard violation for both convex and strongly convex loss functions, where $v$ represents the constraint variation (from $0$ for fixed constraints to $1$ for arbitrary constraints). This hard violation bound recovers the $\mathcal{O}(1)$ violation achievable for fixed constraints in the time-invariant COCO world \textit{at best}. However, compared with the $\mathcal{O}(\sqrt{T}\log{T})$ hard violation achievable for arbitrary constraints \cite{HOCO-Varying:A.Sinha-NeurIPS'24}, this bound degrades to $\mathcal{O}(T)$ in the time-varying world \textit{at worst}.

The significant performance gap between time-invariant and time-varying COCO worlds leads to a fundamental question: \textit{Can a COCO algorithm provide a hard violation bound that guarantees i) $\mathcal{O}(\sqrt{T}\log{T})$ violation for arbitrary constraints at worst, and at the same time, ii) recovers $\mathcal{O}(1)$ violation for fixed constraints at best, thus bridging the best-known hard violations for time-varying and time-invariant COCO worlds?}

**[Move 3 – Occupying the Niche]**

In this work, a new \textit{double-queue} design generates two complementary violation bounds: one robust for arbitrary constraints and one tight for fixed constraints. Their minimum achieves both i) and ii) simultaneously, contrasting with existing single-queue approaches limited to achieving either one. This leads to a hard violation bound that is \textit{never worse} and can be \textit{strictly better} than state-of-the-art COCO algorithms for \textit{any} constraint violation (see detailed comparisons in Table~\ref{tab:1}).

We summarize our main contributions below:

$\bullet$ We propose an efficient algorithm for COCO, handling both time-varying and time-invariant constraints. We name the algorithm \textsc{Double-Q}, since it leverages both an original virtual Queue to construct a surrogate loss and a surrogate virtual Queue to construct a surrogate drift-plus-penalty (SDPP). Unlike existing single-queue COCO approaches, this new double-queue design provides tighter dual control over the constraint violations, even without requiring Slater's condition.

$\bullet$ We analyze the performance of \textsc{Double-Q}, which minimizes an upper bound of the SDPP at each time. Our analysis shows that \textsc{Double-Q} achieves $\mathcal{O}(\sqrt{T})$ regret and $\mathcal{O}(\min\{\sqrt{T}\log{T},T^v\})$ hard violation, where $v$ continuously quantifies the cumulative constraint variation (see its definition in \eqref{eq:V_g}). Notably, \textsc{Double-Q} is the first to simultaneously guarantee $\mathcal{O}(\sqrt{T}\log{T})$ hard violation for arbitrary constraints at worst  ($v=1$) and recover $\mathcal{O}(1)$ hard violation for fixed constraints at best ($v=0$), even without knowing $v$.
	
$\bullet$ We further analyze the performance of \textsc{Double-Q} under strongly convex loss functions. Our analysis shows that \textsc{Double-Q} achieves both improved $\mathcal{O}(\log{T})$ regret and $\mathcal{O}(\min\{\sqrt{T\log{T}},T^v\})$ hard violation. Notably, \textsc{Double-Q} remains the first to simultaneously guarantee $\mathcal{O}(\sqrt{T\log{T}})$ hard violation at worst and recover $\mathcal{O}(1)$ hard violation at best for COCO with strongly convex loss functions.
	
$\bullet$ We conduct numerical experiments to evaluate the performance of \textsc{Double-Q} on various applications including online quadratic programming, online job scheduling, and online fraud detection, with both convex and non-convex losses under real-world datasets. Simulation results demonstrate that \textsc{Double-Q} consistently provides superior performance over state-of-the-art baselines.

---

## Literature Review

**[Move 1 – Thematic Overview]**

The seminal OCO work \cite{OCO:M.Zinkevich-ICML'03} achieved $\mathcal{O}(\sqrt{T})$ static regret to the best fixed decision. Subsequent work \cite{OCO:E.Hazan-ML'07} improved the static regret to $\mathcal{O}(\log{T})$ for strongly convex loss functions. A notion of dynamic regret to a sequence of time-varying decisions was also introduced in \cite{OCO:M.Zinkevich-ICML'03}. Subsequent OCO works developed various algorithms to bound the dynamic regret \mbox{\cite{DOCO:E.C.Hall-JTSP'15}\nocite{DOCO:L.Zhang-NIPS'18}\nocite{DOCO:N.Eshraghi-ICML'20}-\cite{DOCO:L.Zhang-JMLR'24}}. In this work, we focus on bridging the best achievable hard violations in time-invariant \cite{SCOCO-Fix:M.Mahdavi-MLR'12}\nocite{SOCO-Fix:R.Jenatton-ICML'16}\nocite{SOCO-Fix:H.Yu-JMLR'20}\nocite{HOCO-Fix:J.Yuan-NeurIPS'18}\nocite{HOCO-Fix:X.Yi-ICML'21}-\cite{HOCO-Varying:H.Guo-NeurIPS'22} and time-varying COCO~\cite{HOCO-Varying:H.Guo-NeurIPS'22}\nocite{SOCO-Varying:X.Cao-TAC'19}\nocite{SOCO-Varying:M.J.Neely-ArXiv'17}\nocite{HOCO-Varying:A.Sinha-NeurIPS'24}\nocite{SOCO-Varying:T.Chen-TSP'17}\nocite{SOCO-Varying:Q.Liu-SIGMETRICS'22}\nocite{SOCO-Varying:J.Wang-TON'23}\nocite{HOCO-Varying:J.Wang-AAAI'25}-\cite{HOCO-Varying:Lekeufack-ArXiv'24}, under the static regret (regret for short).

**[Move 2 – Critical Analysis]**

### Time-Invariant COCO

Early COCO works focused on known time-invariant constraints and adopted the soft violation metric \cite{SCOCO-Fix:M.Mahdavi-MLR'12}\nocite{SOCO-Fix:R.Jenatton-ICML'16}-\cite{SOCO-Fix:H.Yu-JMLR'20}, which allows compensated constraint violations over time. The saddle-point-type algorithm in \cite{SCOCO-Fix:M.Mahdavi-MLR'12} --- constructing Lagrangian functions followed by primal-dual gradient descent --- achieved $\mathcal{O}(\sqrt{T})$ regret and $\mathcal{O}(T^\frac{3}{4})$ soft violation. Subsequent work~\cite{SOCO-Fix:R.Jenatton-ICML'16} achieved $\mathcal{O}(\max\{T^c,T^{1-c}\})$ regret and $\mathcal{O}(T^{1-\frac{c}{2}})$ soft violation, where $c\in[0,1]$ is a trade-off parameter. The virtual-queue-based algorithm in \cite{SOCO-Fix:H.Yu-JMLR'20} --- constructing virtual queues followed by drift-plus-penalty upper bound minimization --- achieved the best-known $\mathcal{O}(1)$ soft violation under Slater's condition, which excludes important equality constraints in many practical applications.

Other time-invariant COCO works adopted the hard violation metric, which prohibits compensation for constraint violations \cite{HOCO-Fix:J.Yuan-NeurIPS'18}\nocite{HOCO-Fix:X.Yi-ICML'21}-\cite{HOCO-Varying:H.Guo-NeurIPS'22}. The saddle-point-type algorithm in \cite{HOCO-Fix:J.Yuan-NeurIPS'18} achieved $\mathcal{O}(\max\{T^c,T^{1-c}\})$ regret and $\mathcal{O}(T^{1-\frac{c}{2}})$ hard violation. Under Slater's condition, the violation was improved to $\mathcal{O}(T^\frac{1-c}{2})$ \cite{HOCO-Fix:X.Yi-ICML'21}. The lower-bounded virtual queue algorithm in \cite{HOCO-Varying:H.Guo-NeurIPS'22} achieved $\mathcal{O}(1)$ hard violation without Slater's condition.

### Time-Varying COCO

Recent COCO works considered unknown arbitrarily time-varying constraints under both soft \cite{SOCO-Varying:X.Cao-TAC'19,SOCO-Varying:M.J.Neely-ArXiv'17} and hard violation metrics \cite{HOCO-Varying:H.Guo-NeurIPS'22,HOCO-Varying:A.Sinha-NeurIPS'24,HOCO-Varying:Lekeufack-ArXiv'24}. The saddle-point-type algorithm in~\cite{SOCO-Varying:X.Cao-TAC'19} achieved $\mathcal{O}(\sqrt{T})$ regret and $\mathcal{O}(T^\frac{3}{4})$ soft violation without Slater's condition, while the best-known $\mathcal{O}(\sqrt{T})$ soft violation was achieved by the virtual-queue-based algorithm in~\cite{SOCO-Varying:M.J.Neely-ArXiv'17} under Slater's condition. The lower-bounded virtual queue algorithm in~\cite{HOCO-Varying:H.Guo-NeurIPS'22} achieved $\mathcal{O}(\sqrt{T})$ regret and $\mathcal{O}(T^\frac{3}{4})$ hard violation, while the best-known $\mathcal{O}(\sqrt{T}\log{T})$ hard violation was achieved by the surrogate gradient descent algorithm in~\cite{HOCO-Varying:A.Sinha-NeurIPS'24} {and its optimistic version in \cite{HOCO-Varying:Lekeufack-ArXiv'24} (under the standard COCO setting without predictions)}. However, these results reveal a significant $\Omega(\sqrt{T})$ performance gap in constraint violation between the two COCO worlds.

**[Move 3 – Research Gaps]**

Another line of work bridges the two COCO worlds through unified analysis of constraint violations~\cite{SOCO-Varying:T.Chen-TSP'17}\nocite{SOCO-Varying:Q.Liu-SIGMETRICS'22}\nocite{SOCO-Varying:J.Wang-TON'23}-{\cite{HOCO-Varying:J.Wang-AAAI'25}}. Specifically, the modified saddle-point-type algorithm in \cite{SOCO-Varying:T.Chen-TSP'17} achieved $\mathcal{O}(T^\frac{1+v}{2})$ regret and $\mathcal{O}(T^{1-v})$ soft violation under a sufficiently large Slater constant, where $v\in[0,1]$ quantifies constraint variation ($0$: fixed constraints; $1$: arbitrary constraints). Virtual-queue-based algorithms achieved $\mathcal{O}(\sqrt{T})$ regret and $\mathcal{O}(\max\{T^\frac{3}{4},T^v\})$ soft violation without Slater's condition~\cite{SOCO-Varying:Q.Liu-SIGMETRICS'22}, improving to $\mathcal{O}(\max\{T^\frac{1}{2},T^v\})$ soft violation under Slater's condition~\cite{SOCO-Varying:J.Wang-TON'23}. More recently, the doubly-bounded virtual queue algorithm in \cite{HOCO-Varying:J.Wang-AAAI'25} achieved $\mathcal{O}(T^v)$ hard violation without Slater's condition --- recovering $\mathcal{O}(1)$ violation for the first time in the time-varying COCO world. However, this hard violation bound provides no worst-case guarantees for arbitrary constraints, unlike those in \cite{HOCO-Varying:H.Guo-NeurIPS'22, HOCO-Varying:A.Sinha-NeurIPS'24}.

**[Move 4 – Conclusion of the Literature Review]**

Addressing the significant performance gap between the two COCO worlds, we focus on centralized COCO. While distributed COCO has been studied \cite{Dis-COCO:S.Hosseini-TAC'16}\nocite{Dis-COCO:S.Shahrampour-TAC'18}\nocite{Dis-COCO:D.Yuan-TAC'22}-\cite{Dis-COCO:X.Yi-TAC'25}, it maintains centralized performance bounds at best. As Table~\ref{tab:1} demonstrates, \textit{\textsc{Double-Q} bridges the best-known hard violations in the two COCO worlds, outperforming state-of-the-art algorithms}.

---

## Notes

**Research Context:**
This paper focuses on bridging the performance gap between time-invariant and time-varying Constrained Online Convex Optimization (COCO), specifically addressing hard constraint violations. The Double-Q algorithm represents a novel double-queue design that achieves the best of both worlds.

**Key Technical Innovation:**
The main innovation is using two virtual queues (original queue + surrogate queue) instead of traditional single-queue approaches. This provides complementary violation bounds that can adapt to different constraint variation levels.

**Target Venue:**
This work is intended for submission to a top-tier machine learning/optimization conference (e.g., NeurIPS, ICML, or ICLR).

**Next Steps:**
- Complete the methodology section describing the Double-Q algorithm in detail
- Provide complete theoretical analysis and proofs
- Conduct comprehensive experiments
- Write conclusion and future work sections
