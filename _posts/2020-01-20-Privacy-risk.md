---
layout:     post
mathjax: true
title:      Pricavy Risks of Securing Machine Learning Models against Adversarial Examples
# subtitle:   如何切换Xcode命令行工具
date:       2020-01-20
author:     Jiahao Yu
header-img: img/post-bg-kuaidi.jpg
catalog: true
tags:
    - CCS2019
    - Membership Inference
    - Adversarial examples
---

# SUMMARY

This paper demonstrates that an adversarially trained model is more easily exposed to membership inference attack. The author does a lot of experiments to verify this. Detailly, the contributions can be summarized as follows:

- The author proposes two new inference attack algorithms based on adversarial examples. Instead of using benign data points to do the inference, the author uses untargeted and targeted adversarial examples to infer the robust model. The generated adversarial examples are constrained with $\epsilon$. Notice that here the author points out that the $\epsilon$ does not need to be the exact adversarial pertubation defined during adversarial training.

- It verifies its claim by analysing the sensetivity of standard models and robust models. It finds that a robust model is more sensitive thus it may leak more membership infomation.

- It does membership inference attack against six types of robust models and find that they indeed leak more privacy of membership infomation. The author also gives a detailed analysis of PGD-based adversarially trained models and find that:

~~~
1. A larger pertubation budget lead to higher risk of membership inference risk.
2. As more data points are used for adversarial training, the robust model leaks more privacy.
3. AS the model capacity grows, the robust model also leaks more membership infomation.
~~~

- The author verifies that targeted inference attack can have a better performance than untargeted inference attack.

- The author does some experiments beyond image classification and finds that the claim stands.

- Some tips are given to defend such attack, like temperature scaling and regularization.

- The author claims that pixel dp is also exposed to such threats. Instead


# MY OPINION

## ADVANTAGE:

The author does ***a lot of*** experiments that make his analyse really comprehensive. The workload impresses me a lot that the paper indeed deserves acceptance.

## DISADVANTAGE:

The core idea seems to be a little straightfoward. From previous work, we know that the membership inference advantage can be directly related with generalization error. The following flow is easy to know:
```flow
st=>start: Robust training
op=>operation: Larger generalization gap
op_2=>operation: Higher membership risk
e=>end
st->op->op_2->e
```
However, it's still very interesting to propose this theory. Maybe we can investigate some methods to guarantee a both robust and private model.