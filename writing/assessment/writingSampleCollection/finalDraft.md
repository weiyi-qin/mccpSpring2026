# Constrained Online Convex Optimization: Keeping Pace with Dynamics of Both Loss and Constraint

## INTRODUCTION

**[Move 1 - Establishing a Territory]** Online Convex Optimization (OCO), which represents a state of the art at the intersection of machine learning, operations research and game theory, has become the center of attention to model sequential decision-making problems under uncertainty (Hazan, 2016; Shalev-Shwartz, 2012). In practice, decision-makers are regularly expected to implement a sequence of decisions with incomplete information and constantly changing conditions, and the general goal thereof is the reduction of cumulative loss in the long run. Since the application scenarios have been more complicated, the basic OCO framework has naturally expanded into the Constrained Online Convex Optimization (COCO). This highly developed model has a lot of practical significance to such critical systems as advertisement placement (Balseiro, Lu, and Mirrokni, 2020), load balancing (Hsu et al., 2021), network virtualization (Shi, 2021, Lin, and Fahmy, 2021), and resource allocation (Wang et al., 2023). Environmental dynamism is the rule and not the exception in these complex systems since the electricity demands vary across time or the market prices also vary. As a result, there is a dire need to ensure that the optimisation algorithms are agile enough to capture (and adapt to) the dynamic changes in both loss functions and constraint conditions in the acute sense.

**[Move 2 - Identifying a Niche]** As much theoretical and practical progress has been made to date with the connection of the thing of existing COCO algorithms, the most recent body of literature has a number of strong limitations that restrict their usage in real-world systems that are highly dynamic. First, it is important to note that most of the most modern algorithms that are created to address time-changing constraints heavily depend on the Slater condition (Chen, Ling, and Giannakis, 2017; Yu, Neely, and Wei, 2017). The Slater condition is a condition which assumes that there is a strictly feasible interior point which satisfies all the constraints with a margin. The current literature is based mostly on the measure of the so-called soft constraint violation or long-term constraints when examining the issue of constraint violations (Mahdavi, Jin, & Yang, 2012; Jenatton, Huang, and Archambeau, 2016). This paradigm allows the compensation of violations at some of the time steps through strict conformity at other points in time. Although mathematically convenient, it is seriously flawed in safety-critical applications. The current non-closed gap in the current literature concerning the realisation of the optimal dynamic regret whilst strictly addressing violation of hard constraints but not relying on Slater condition is deep and unresolved especially in the context of environment that is characterised by the dual dynamics of both loss and constraint functions (Guo et al., 2022; Sinha and Vaze, 2024).

**[Move 3 - Occupying the Niche]** To fill these abovementioned research gaps, in this study, we will introduce a new online learning algorithm, which is called Constrained Online Learning with Doubly bound Queue (COLDQ). Having a strictly constraining mechanism of violating hard constraints and minimising dynamic regret in dynamic environments is the main aim of this research and has no dependence on the restrictive Slater condition. The proposed algorithm allows controlling violations of the constraints in a tight and instantaneous controlled manner by at once implementing the lower and upper bounds on the virtual queue. This paper proves that the COLDQ algorithm is capable of achieving optimal dynamic regret and hard constraint violation bounds which smooth to the best-known theoretical limits with a shrinking dynamics of the losses and constraints by a novel Lyapunov drift analysis. Also, this study presents a variant of COLDQ called expert-tracking, and thus, it offers a strong solution since it meets the same performance limits without pre-knowledge of the system dynamics.

## LITERATURE REVIEW

**[Move 1 - Thematic Overview]** This paper seeks to review and integrate applicable literature on the area of Constrained Online Convex Optimization (COCO) with specific focus being placed on the theoretical development of algorithms and the inherent constraints on algorithms attempting to handle a time-varying constraint and dynamic setting. To determine the extent of the scope of this review, the analysis will be framed on two main performance definitions: dynamic regret (the cumulative loss difference between the decisions and optimal dynamic choices of an algorithm) and hard constraint violation (the cumulative non-negative difference in constraint violation). The available literature is divided into three major categories: (i) online convex optimization and stationary regret; (ii) online learning with soft/long term constraints; and (iii) recent developments in the area of more dynamic regret and hard constraints. The critical analysis of these themes pursues to highlight the theoretical choke points that the existing approaches currently face in the process of dealing with both dynamics, in order to build a strong theoretical underpinning to the suggested COLDQ algorithm.

**[Move 2 – Critical Analysis]** The initial studies in OCO had focused on unconstrained optimisation problems or ones constrained by fixed, time-invariant feasible region. The first entry of Zinkevich (2003) provided the algorithm of Online Gradient Descent (OGD), which has a timeless regret of the order of O(T) on the condition of general convexity. Later research improved this model and reached logarithmic regret in strongly convex functions (Hazan, Agarwal & Kale, 2007). The first flaw inherent to these classical algorithms is that the evaluation criterion, which is known as the regret, is that against one reference point, optimum decision that is known only in hindsight. The best decision in especially dynamic environments changes much more across time; as a result, the more restrictive concept of dynamic regret is needed instead of the less restrictive concept of static regret (Jadbabaie et al., 2015; Mokhtari et al., 2016; Zhang et al., 2017).

Mahdavi, Jin and Yang (2012) were the first to introduce the concept of long-term constraints, to meet time-varying constraints and minimize the computational costs of projection operations. This paradigm allows transient constraints violations as long as the growth rate of the accumulating violation along the horizon is sublinear. In this context, soft constraint violation bounds can be bounded with virtual-queue methods based on Lyapunov optimisation, and these approaches have been extensively used in this context (Yu and Neely, 2020). Time-varying constraints In the case of time-varying constraints, various studies have proposed an algorithm based on saddle points or virtual queues to obtain sublinear static error and soft constraint violations (Cao, Zhang and Poor, 2021; Wei, Yu and Neely, 2020).

Over the past few years, there has been a push by the researchers to place more restrictive performance measures, and attempt to set a limit on both dynamic regret and hard constraint violation. Yuan and Lamperski (2018) proposed a more demanding type of hard constraint violation, whereby the violation cannot be tolerated through compensation. Under non-variable constraints, Guo et al. (2022) were able to obtain the best-known O(1) violation of hard constraints by maintaining O(T) of the regret that is not dynamic. Recent research has gone a long way in the context of time-varying constraints. Yi et al. (2021) and Yi et al. (2023) analyzed regret and accumulated constraint violation in a distributed environment. More recently, Sinha and Vaze (2024) obtained the modern best O (T log T) hard constraint violation and O (T) static regret of adversarial constraints. Even though these algorithms have been able to achieve sublinear dynamic regret guarantees (Zhao & Zhang, 2021; Zhang, Lu and Zhou, 2018), the methods to regulate hard constraint violations in nearly all cases rely on the Slater condition or cannot eliminate the optimal O 1 violation as dynamics in the system get smaller.

**[Move 3 – Research Gaps]** An overall review of the literature mentioned above demonstrates that there is a drastic gap in the theoretical inlays of the COCO sphere. Precisely, as the dynamics of the loss and constraint functions weaken, none of the current hard constraint violation bounds of time-varying constraints converges to the best-known O (1) violation of fixed constraint problems (Guo et al., 2022; Sinha and Vaze, 2024). Moreover, the existing literature lacks an effective mechanism that can facilitatively regulate the hard constraint violations and at the same time achieve optimal dynamic regret limits without Slater condition dependency. Single-bounded virtual queues have an inherent inadequacy to deal with the harsh dual dynamics of simultaneously varying losses and constraints.

**[Move 4– End of the Literature Review]** To sum up, both traditional static regret analyses and the soft constraint models are now no longer adequate to the more demanding requirements of today sophisticated, dynamic systems. At the same time, current dynamic COCO algorithms are still severely crippled by the reliance on the extraneous Slater condition and failure to deal with the weakening system dynamics. This scenario highlights the urgency to work on new constraint-handling mechanisms. It is necessary to overcome this bottleneck in theory, which involves a radical redesign of the old virtual queue design. This paper will attempt to reduce reliance on Slater condition by presenting a doubly-bounded queue which only limits the lower and upper bounds of the queue. By so doing, it aims to give unparalleled, seamless and tight theoretical assurances in both dynamic regret and hard constraint breaches in environments that are dual dynamic in nature.

Words: 1489

## REFERENCES

Balseiro, S., Lu, H., & Mirrokni, V. (2020). Dual mirror descent for online allocation problems. In Proceedings of the 37th International Conference on Machine Learning (ICML) (pp. 613-628).

Cao, X., & Liu, K. J. R. (2019). Online convex optimization with time-varying constraints and bandit feedback. IEEE Transactions on Automatic Control, 64(7), 2665-2680.

Cao, X., Zhang, J., & Poor, H. V. (2021). Constrained online convex optimization with feedback delays. IEEE Transactions on Automatic Control, 66(11), 5049-5064.

Chen, T., Ling, Q., & Giannakis, G. B. (2017). An online convex optimization approach to proactive network resource allocation. IEEE Transactions on Signal Processing, 65(24), 6350-6364.

Eshraghi, N., & Liang, B. (2020). Distributed online optimization over a heterogeneous network with any-batch mirror descent. In Proceedings of the 37th International Conference on Machine Learning (ICML) (pp. 2933-2942).

Guo, H., Liu, X., Wei, H., & Ying, L. (2022). Online convex optimization with hard constraints: Towards the best of two worlds and beyond. In Advances in Neural Information Processing Systems (NeurIPS) (pp. 36426-36439).

Hall, E. C., & Willett, R. M. (2015). Online convex optimization in dynamic environments. IEEE Journal of Selected Topics in Signal Processing, 9(4), 647-662.

Hazan, E. (2016). Introduction to online convex optimization. Foundations and Trends in Optimization, 2(3-4), 157-325.

Hazan, E., Agarwal, A., & Kale, S. (2007). Logarithmic regret algorithms for online convex optimization. Machine Learning, 69(2), 169-192.

Hsu, W.-K., Xu, J., Lin, X. L., & Bell, M. R. (2021). Integrated online learning and adaptive control in queueing systems with uncertain payoffs. Operations Research, 70(2), 1166-1181.

Jadbabaie, A., Rakhlin, A., Shahrampour, S., & Sridharan, K. (2015). Online optimization: Competing with dynamic comparators. In Proceedings of the 18th International Conference on Artificial Intelligence and Statistics (AISTATS) (pp. 398-406).

Jenatton, R., Huang, J., & Archambeau, C. (2016). Adaptive algorithms for online convex optimization with long-term constraints. In Proceedings of the 33rd International Conference on Machine Learning (ICML) (pp. 402-411).

Liu, Q., Wu, W., Huang, L., & Fang, Z. (2022). Simultaneously achieving sublinear regret and constraint violations for online convex optimization with time-varying constraints. ACM SIGMETRICS Performance Evaluation Review, 49(3), 4-5.

Mahdavi, M., Jin, R., & Yang, T. (2012). Trading regret for efficiency: Online convex optimization with long term constraints. The Journal of Machine Learning Research, 13(1), 2503-2528.

Mokhtari, A., Shahrampour, S., Jadbabaie, A., & Ribeiro, A. (2016). Online optimization in dynamic environments: Improved regret rates for strongly convex problems. In Proceedings of the 55th IEEE Conference on Decision and Control (CDC) (pp. 7195-7201).

Shalev-Shwartz, S. (2012). Online learning and online convex optimization. Foundations and Trends in Machine Learning, 4(2), 107-194.

Shi, M., Lin, X., & Fahmy, S. (2021). Competitive online convex optimization with switching costs and ramp constraints. IEEE/ACM Transactions on Networking, 29(2), 876-889.

Sinha, A., & Vaze, R. (2024). Optimal algorithms for online convex optimization with adversarial constraints. In Advances in Neural Information Processing Systems (NeurIPS).

Wang, J., Dong, M., Liang, B., Boudreau, G., & Abou-Zeid, H. (2023). Delay-tolerant OCO with long-term constraints: Algorithm and its application to network resource allocation. IEEE/ACM Transactions on Networking, 31(1), 147-163.

Wei, X., Yu, H., & Neely, M. J. (2020). Online primal-dual mirror descent under stochastic constraints. Proceedings of the ACM on Measurement and Analysis of Computing Systems (POMACS), 4(2), 1-36.

Yi, X., Li, X., Yang, T., Xie, L., Chai, T., & Johansson, K. (2021). Regret and cumulative constraint violation analysis for online convex optimization with long term constraints. In Proceedings of the 38th International Conference on Machine Learning (ICML) (pp. 11998-12008).

Yi, X., Li, X., Yang, T., Xie, L., Chai, T., & Johansson, K. H. (2023). Regret and cumulative constraint violation analysis for distributed online constrained convex optimization. IEEE Transactions on Automatic Control, 68(5), 2875-2890.

Yu, H., & Neely, M. J. (2020). A low complexity algorithm with O(T) regret and O(1) constraint violations for online convex optimization with long term constraints. Journal of Machine Learning Research, 21(1), 1-24.

Yu, H., Neely, M., & Wei, X. (2017). Online convex optimization with stochastic constraints. In Advances in Neural Information Processing Systems (NeurIPS) (pp. 1428-1438).

Yuan, J., & Lamperski, A. (2018). Online convex optimization for cumulative constraints. In Advances in Neural Information Processing Systems (NeurIPS) (pp. 6140-6149).

Zhang, L., Lu, S., & Zhou, Z.-H. (2018). Adaptive online learning in dynamic environments. In Advances in Neural Information Processing Systems (NeurIPS) (pp. 1330-1340).

Zhang, L., Yang, T., Yi, J., Jin, R. J., & Zhou, Z.-H. (2017). Improved dynamic regret for non-degenerate functions. In Advances in Neural Information Processing Systems (NeurIPS) (pp. 732-741).

Zhao, P., & Zhang, L. (2021). Improved analysis for dynamic regret of strongly convex and smooth functions. In Proceedings of the 3rd Conference on Learning for Dynamics and Control (L4DC) (pp. 48-59).

Zinkevich, M. (2003). Online convex programming and generalized infinitesimal gradient ascent. In Proceedings of the 20th International Conference on Machine Learning (ICML) (pp. 928-936).

## Declaration of Generative AI and AI-assisted technologies in the writing process

During the preparation of this work the author used DeepSeek and ChatGPT in order to assist in improving grammar, clarity, and academic tone of the manuscript. After using this tool, the author(s) reviewed and edited the content as needed and took full responsibility for the content of the publication.

The specific tasks are as follows:

- Correct colloquial expressions and incorrect vocabulary, using more academic language.
- Correct basic grammatical errors, spelling mistakes, and improper punctuation.
- Enhance the connections and logic between sentences, avoid redundancy, and improve the fluency of the text.
- Adjust some overly subjective expressions to a more objective and neutral academic tone.
- Check the accuracy of reference citations in the manuscript, and ensure that the order of references in the appendix corresponds to the order of citations in the original text.
