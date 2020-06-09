## 简介

机器模型大多是黑箱模型，很难去解释变量和模型之间的关系。通过不同的方法，可以使模型的解释性更强。 在树形模型中，通常用变量重要性去衡量每个变量的重要程度。

## Packages
- Eli5
- PDP Box
- Shap
Eli5 和PDP Box主要是针对变量的重要性；Shap可以可视化单条记录每个变量的贡献

## Eli5 （Permutation Importance)
主要是通过打乱变量的顺序重新预测，看新预测值和源模型的区别。如果变量的顺序被打乱，模型效果提高便说明这个变量对模型没有影响。

## PDP Box （Partial Dependent Plot）

PDP 主要探讨的是变量的边际变化：即这个变量变动一个单位对最后预测结果有什么影响。

主要function：
- info_graph.target_plot : 变量原始分布
- info_graph.actual_plot : 变量分布和模型预测结果的分布
- pdp.pdpplot : 变量变动单位对预测结果的影响

## Shap

Shap 是博弈论的一个概念，主要是值参与游戏的每一个人对结论有什么贡献。利用shap 可以可视化每一个样本的预测结果中每一个变量有什么样的贡献。
- Force Plot : 单条记录下每个变量对每个预测值的影响
- Summary Plot : 整个数据集每个变量对每个预测值的影响
