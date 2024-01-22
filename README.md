This is the code implementation of the random renormalization group presented in the paper entitled as "Fast renormalizing the structures and dynamics of ultra-large systems via random renormalization group".

The abstract of this paper is shown below:

Criticality and symmetry, studied by the renormalization groups, lie at the heart of modern physics theories of matters and complex systems. However, surveying these properties with massive experimental data is bottlenecked by the intolerable costs of computing renormalization groups on real systems. Here, we develop a time- and memory-efficient framework, termed as the random renormalization group, for renormalizing ultra-large systems (e.g., with millions of units) within minutes. This framework is based on random projections, hashing techniques, and kernel representations, which support the renormalization governed by linear and non-linear correlations. For system structures, it exploits the correlations among local topology in kernel spaces to unfold the connectivity of units, identify intrinsic system scales, and verify the existences of symmetries under scale transformation. For system dynamics, it renormalizes units into correlated clusters to analyze scaling behaviours, validate scaling relations, and investigate potential criticality. Benefiting from hashing-function-based designs, our framework significantly reduces computational complexity compared with classic renormalization groups, realizing a single-step acceleration of two orders of magnitude. Meanwhile, the efficient representation of different kinds of correlations in kernel spaces realized by random projections ensures the capacity of our framework to capture diverse unit relations. As shown by our experiments, the random renormalization group helps identify non-equilibrium phase transitions, criticality, and symmetry in diverse large-scale genetic, neural, material, social, and cosmological systems.

Two Jupyter notebook files are released as the instances of applying the random renormalization group on dynamics and structure renormalization. The full descriptions of all functions in this files can be seen in the attached PDF file, which is the supplementary material of the paper.
