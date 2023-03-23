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

Input Embedding Layer                      
Positional Encoding Layer              
Transformer Encoder Layers                    
Classification Head                        

![image](https://user-images.githubusercontent.com/48261978/227057387-5a719ced-f5f1-4ac7-a944-877ec36d37bd.png)

1. images are split into "patches" which act as sequence tokens in this case
2. patches are flattened
3. get linear embedding from patches
4. add positional embeddings to the patches
5. feed into a transformer encoder
6. pretrain using labeled images
7. finetune model later for image classification


## Solution

### Helpful Properties of MSAs:            
• MSAs flatten the loss landscape                     
• A key feature of MSAs is data specificity               

### How do MSAs and Convs behave?

MSAs use low-frequency signals and Convs use high-frequency signals.
MSAs are low-pass filters, and Convs are high-pass filters.               

MSAs generally reduce the high-frequency component of feature map, and MLPs (corresponding to Convs) amplify it.                    

![image](https://user-images.githubusercontent.com/48261978/227226385-67616c89-5994-4b10-bd0d-da50af2e8bd7.png)

MSAs aggregate feature maps, but Convs do not.                                   
MSAs capture global relationships and patterns across all positions, meaning they aggregate information from all positions and combine it into a single feature map.                             
Convs capture local patterns, meaning they aggregate patterns/variations with each region of the input image.                                     


*Question: Would MSAs and Convs work together?* 


Advantage compared to CNNs: MSAs better capture local features and long-range dependencies                       

Disadvantage compared to CNNs: Less efficient and requires significantly more memory                     


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
3. Authors propose AlterNet, a model that replaces Conv blocks at the end of a stage with MSA blocks. AlterNet outperforms CNN models in both large and small datasets.





## Analysis

The title of the article is misleading, because I assumed the authors would talk about vision transofrmers as a whole. Instead, the authors mainly focused on the multi-headed self-attention layers, and it was all in relation to Convs. 

## Resources                 

How Do Vision Transformers Work?: https://arxiv.org/pdf/2202.06709v1.pdf                                     
Kaggle CiFar10 ViT example: https://www.kaggle.com/code/lonnieqin/cifar10-classification-vision-transformer/notebook
