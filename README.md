# Transformers-and-shortcut-learning

Transformers as an architecture have shown a lot of promise over the years, increasingly in the field of vision.
However, recent studies have shown that they are not immune to shortcut learning, which is quite problematic, given how transformers are increasingly being used
for medical purposes. Therefore, I've tried to study how susceptible Vision Transformers are to shortcut learning, by taking the classic and simple cats vs dogs dataset from MSR.

My goal is to replicate shortcut learning in a rather simple way which nevertheless fools the transformer into learning spurious correlations.
I've trained the same architecture (A ViT with a couple of encoder blocks and 6 heads in each block) following the standard considerations as described in the original paper on two different datasets:
1) The original cats vs dogs dataset
2) A slightly modified version of the cats vs dogs dataset. (**Where no images of cats or dogs were modified but only very small shortcuts were added**) 

This modified version is exactly the same as the original except I've randomly added small shortcuts to the original. These shortcuts are so small that an inattentive observer might not even 
know that the original dataset has been modified. Here are the preliminary results I got - 

## Comparison of test accuracies on a hold out set for a model trained on the datasets 

![image](https://github.com/Ruthvik9/Transformers-and-shortcut-learning/assets/74010232/7578a072-ff2f-4c27-8993-a4bb6a73cce6)

And the following are the corresponding loss values during training -

![image](https://github.com/Ruthvik9/Transformers-and-shortcut-learning/assets/74010232/32262c7d-a424-4730-b4ae-dc6f31c4b07c)

It is evident that while the test accuracy for the model trained on the very slightly modified dataset (where no images of cats or dogs were modified but only very small shortcuts were added) increases first as expected, it begins to rapidly fall, indicating the model's susceptibility to shortcut learning. This phase can also be seen in how the model's loss values on the training set rapidly decrease in one region. 
Contrary to this, the same model (with the same architecture, hyperparameters etc.) performs better and as expected on an unmodified dataset.



Much much more interestingly (to me atleast, this problem doesn't seem to occur when I'm using He initialization)

## Results using He initialization - 

![image](https://github.com/Ruthvik9/Transformers-and-shortcut-learning/assets/74010232/ebb0dda8-6540-43c8-a790-39b65a351062)


![image](https://github.com/Ruthvik9/Transformers-and-shortcut-learning/assets/74010232/b93b7a4b-4c7c-4261-9df8-fbf2c517571b)



 


I'm currently trying to run more ablation experiments to analyse this behavior further and come up with new components which help the transformer combat this phenomenon.

 
