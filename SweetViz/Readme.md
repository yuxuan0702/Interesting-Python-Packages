## 简介

SweetViz是一个类似于Pandas_Profiling的一键式生成基础EDA的包。主要一共有三个Function: Analyze，Compare 和Compare_Intra. 

## Package源页面

Github 文件页面： https://github.com/fbdesignpro/sweetviz

## SweetViz 特点

1. 可以探测目标变量和剩余变量的联系
2. 可以比较两个不同数据集的数据特征（训练集和测试集）和同一数据集的不同的选项的比较（男性vs女性）
3. 不同类数据的相关性
   - 数字变量计算pearson系数
   - 文字变量计算相关系数（百分比相关系数，卡方检验）

4. 变量类型检测： 自动检测变量是数字变量，文字变量还是序数变量
5. 基础信息描述： 最大最小值平均数，中位数和众数标准差，方差

## 安装

Win： Anaconda 终端

Mac：终端

```shell
pip install sweetviz 
```

## 基本运用

1. **Analyze**

   ```python
   sv.analyze(source: Union[pd.DataFrame, Tuple[pd.DataFrame, str]],
               target_feat: str = None,
               feat_cfg: FeatureConfig = None,
               pairwise_analysis: str = 'auto'):
   ```

   - Source : 想要可视化的数据集

   - target_feat: 文字变量，是分析的目标变量。 通常是二元变量。目前暂时不支持数字变量 

   - feat_cfg: 通常是表示想要省略可视化的变量比如（ID）;

   - Pairwise Analysis: 相关性分析

 

2. **Compare**

   Compare 主要用于比较两个数据集的不同

```python
#compare语法
sv.compare(source:[dataframe,'name you want to present'],
           compare:[dataframe,'name you want to present'],
           target_feat: str = None, 
           feat_cfg: sweetviz.feature_config.FeatureConfig = None, 
           pairwise_analysis: str = 'auto')
```

- Source: 原始数据集
- Compare:想比较的数据集


3. **Compare_Intra** 

Compare_Intra 用于比较一个数据集中某个选项的数据集的不同

```python
#比较不同数据种类的数据集
compare_intra(source_df: pandas.core.frame.DataFrame, condition_series: pandas.core.series.Series, names: Tuple[str, str], target_feat: str = None, feat_cfg: sweetviz.feature_config.FeatureConfig = None, pairwise_analysis: str = 'auto')
```

- Condition: 变量满足什么条件
- names: 变量中所包含的种类类别


4. **代码示例**

```python
# import packages
import pandas as pd
import sweetviz as sv

#import dataset 
df = pd.read_csv('titanic.csv')

#设置跳过passengerID
feature_config = sv.FeatureConfig(skip="PassengerId")

#sv可视化
sv_report = sv.analyze(df,target_feat = 'Survived',feat_cfg = feature_config)
sv_report.show_html()

# 比较训练集测试集有什么不同
compare_two_df = sv.compare([train,'train'],[test,'test'],'Survived')
compare_two_df.show_html()

# 比较男性和女性在分布上有什么不同
report = sv.compare_my_report = sv.compare_intra(df, df["Sex"] == "male", ["Male", "Female"])
report.show_html()
```

