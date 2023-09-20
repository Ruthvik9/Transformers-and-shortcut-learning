# Transformers-and-shortcut-learning

Transformers as an architecture have shown a lot of promise over the years, increasingly in the field of vision.
However, recent studies have shown that they are not immune to shortcut learning, which is quite problematic, given how transformers are increasingly being used
for medical purposes. Therefore, I've tried to study how susceptible Vision Transformers are to shortcut learning, by taking the classic and simple cats vs dogs dataset from MSR.

My goal is to replicate shortcut learning in a rather simple way which nevertheless fools the transformer into learning spurious correlations.
I've trained the same architecture (A ViT with a couple of encoder blocks and 6 heads in each block) following the standard considerations as described in the original paper on two different datasets:
1) The original cats vs dogs dataset
2) A slightly modified version of the cats vs dogs dataset.

This modified version is exactly the same as the original except I've randomly added small shortcuts to the original. These shortcuts are so small that an inattentive observer might not even 
know that the original dataset has been modified. Here are the preliminary results I got - 



I'm currently trying to run more ablation experiments to analyse this behavior further and come up with new components which help the transformer combat this phenomenon.
