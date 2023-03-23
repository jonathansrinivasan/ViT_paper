# **How Do Vision Transformers Work?**
**By Namuk Park, Songkuk Kim**

## Problem

How do Vision Transformers (ViTs) work with Multi-Head Self-Attentions (MSAs)?
 
## Approach

The authors explore:
1. What properties of MSAs do we need to improve optimization?
2. Do MSAs act like Convs?
3. How can we harmonize MSAs with Convs?

## ViT Architecture

Encoder-Only Transformer

Input: images        
Ouput: fixed-dimensional feature vector

![image](https://user-images.githubusercontent.com/48261978/227057387-5a719ced-f5f1-4ac7-a944-877ec36d37bd.png)

1. images are split into "patches" which act as sequence tokens in this case
2. patches are flattened
3. get linear embedding from patches
4. add positional embeddings to the patches
5. feed into a transformer encoder
6. pretrain using labeled images
7. finetune model later for image classification


## Solution



Question: Would MSAs and Convs work together?


#### Advantages compared to CNNs:


#### Disadvantages compared to CNNs:


### AlterNet

A model that unifies ViTs and CNNs by adjusting the ratios of MSAs and Convs.

Design:                       
• Replace Conv blocks with MSA blocks from the end of a baseline CNN model.                  
• If the added MSA block does not improve predictive performance, replace a Conv block located at the end of an earlier stage with an MSA block.             
• Use more heads and higher hidden dimensions for MSA blocks in late stages.           

![image](https://user-images.githubusercontent.com/48261978/227204038-63cc3128-0ef6-408f-8b28-a30df8cea6d4.png)


![image](https://user-images.githubusercontent.com/48261978/227081247-bdc4498c-d251-44b8-a943-8044850aed22.png)


### Takeaways 

1. MSAs improves accuracy and generlization by flattening loss landscapes. ViTs suffer from non-convex losses, which can be fixed with large datasets and loss landscape smoothing methods.
2. MSAs and Conv have opposite behaviors, therefore, they are complementary.
3. Authors propose ALterNet, a model that replaces Conv blocks at the end of a stage with MSA blocks. AlterNet outperforms CNN models in both large and small datasets.





## Analysis

The title of the article is misleading, because I assumed the authors would talk about vision transofrmers as a whole. Instead, the authors mainly focused on the multi-headed self-attention layers, and it was all in relation to Convs. 

## Resources

