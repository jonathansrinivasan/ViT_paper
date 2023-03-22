# **How Do Vision Transformers Work?**
**By Namuk Park, Songkuk Kim**

## Problem

How do Vision Transformers (ViTs) work with Multi-Head Self-Attentions (MSAs)?
 
## Approach

The authors explore:
1. What properties of MSAs do we need to improve optimization?
2. Do MSAs act like Convs?
3. How can we harmonize MSAs with Convs?

## Solution

### Architecture

Encoder-Only Transformer

![image](https://user-images.githubusercontent.com/48261978/227056915-01d6235e-f658-4b5e-ba73-ca3acb4e01f2.png)


Input: images        
Ouput: fixed-dimensional feature vector

### Takeaways 

1. MSAs improves accuracy and generlization by flattening loss landscapes. ViTs suffer from non-convex losses, which can be fixed with large datasets and loss landscape smoothing methods.
2. MSAs and Conv have opposite behaviors, therefore, they are complementary.
3. Multi-stage neural networks behave like a series of small individual models. 
4. Authors propose ALterNet, a model that replaces Conv blocks at the end of a stage with MSA blocks. AlterNet outperforms CNN models in both large and small datasets.

## Analysis

## Resources

