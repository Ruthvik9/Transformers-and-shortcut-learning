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


## Architecture 

----------------------------------------------------------------
        Layer (type)               Output Shape         Param #
================================================================
            Conv2d-1          [-1, 516, 16, 16]         396,804
       BatchNorm2d-2          [-1, 516, 16, 16]           1,032
    PatchEmbedding-3             [-1, 256, 516]               0
           Dropout-4             [-1, 257, 516]               0
         LayerNorm-5               [-1, 2, 516]           1,032
MultiheadAttention-6  [[-1, 2, 516], [-1, 257, 257]]               0
           Dropout-7               [-1, 2, 516]               0
         LayerNorm-8             [-1, 257, 516]           1,032
            Linear-9             [-1, 257, 516]         266,772
             ReLU-10             [-1, 257, 516]               0
           Linear-11             [-1, 257, 516]         266,772
          Dropout-12             [-1, 257, 516]               0
TransformerEncoder-13             [-1, 257, 516]               0
        LayerNorm-14               [-1, 2, 516]           1,032
MultiheadAttention-15  [[-1, 2, 516], [-1, 257, 257]]               0
          Dropout-16               [-1, 2, 516]               0
        LayerNorm-17             [-1, 257, 516]           1,032
           Linear-18             [-1, 257, 516]         266,772
             ReLU-19             [-1, 257, 516]               0
           Linear-20             [-1, 257, 516]         266,772
          Dropout-21             [-1, 257, 516]               0
TransformerEncoder-22             [-1, 257, 516]               0
        LayerNorm-23               [-1, 2, 516]           1,032
MultiheadAttention-24  [[-1, 2, 516], [-1, 257, 257]]               0
          Dropout-25               [-1, 2, 516]               0
        LayerNorm-26             [-1, 257, 516]           1,032
           Linear-27             [-1, 257, 516]         266,772
             ReLU-28             [-1, 257, 516]               0
           Linear-29             [-1, 257, 516]         266,772
          Dropout-30             [-1, 257, 516]               0
TransformerEncoder-31             [-1, 257, 516]               0
        LayerNorm-32             [-1, 257, 516]           1,032
           Linear-33                    [-1, 1]             517
================================================================
Total params: 2,006,209
Trainable params: 2,006,209
Non-trainable params: 0



 


I'm currently trying to run more ablation experiments to analyse this behavior further and come up with new components which help the transformer combat this phenomenon.

 
