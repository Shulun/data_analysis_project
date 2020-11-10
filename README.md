## 游戏用户流失率预测

影响活跃用户流失率的因素：

* 在线活跃
* 用户属性（性别，好友数，等级，积分）
* 游戏情况（游戏局数，获胜局数，失利局数，最高牌类型）

### XGBoost

![XGBoost confusion matrix](https://cdn.jsdelivr.net/gh/shulun/cdn/data_analysis_project/xgboost_cm.png)

![XGBoost feature importance](https://cdn.jsdelivr.net/gh/shulun/cdn/data_analysis_project/xgboost_feature_importance.png)

![XGBoost sample tree](https://cdn.jsdelivr.net/gh/shulun/cdn/data_analysis_project/xgboost_sample_tree.png)

### LightGBM

![LightGBM confusion matrix](https://cdn.jsdelivr.net/gh/shulun/cdn/data_analysis_project/lightgbm_cm.png)

![LightGBM feature importance](https://cdn.jsdelivr.net/gh/shulun/cdn/data_analysis_project/lightgbm_feature_importance.png)

![LightGBM sample tree](https://cdn.jsdelivr.net/gh/shulun/cdn/data_analysis_project/lightgbm_sample_tree.png)


## A/B测试

执行一个A/B测试的一般步骤：

1. 将用户随即分成不同的两组，控制组和测试组；
2. 将变化后的页面分配给测试组，原页面分配给控制组；
3. 开始测试并收集足够数量的样本（样本量由效果量effect size，显著性significance和统计检定力power来决定）；
4. 计算关键度量key metrics并判断影响是否显著；
5. 如果有优胜者，将优胜页面发布。

A/B测试一次只能测试局部的一个变量。如果要测试两个或两个以上的变量或版本，可以采用A/B/n（A/B/C，A/B/C/D等）测试的方式。测试的步骤和上述的步骤一致，不同的地方在于A/B/n需要把用户随即分成更多的组，因而需要更大的流量来确保最终结果的显著性和准确性。

## 多变量测试 Multivariate Testing (MVT)

多变量测试测试了选定变量的所有组合。例如有一个网页，变量A登录按钮有3种颜色选择，变量B网页背景色有2种选择，则多变量测试最终需要测试$3\times2=6$种组合。这就要求测试网站提供更大的流量来满足每一组测试对显著性的需求。

## 因子设计 Factorial Design

在多变量测试的基础上还可以采取因子设计的方式，选择由A/B测试得到的优胜变量值并将它们组合在一起或相互对照实验，来检验该组合或某种变量选择的影响是否更为显著。换种说法，就是只选取多变量测试里面所有组合的子集来进行比对实验。相对来讲，这种测试方法更为灵活，且不需要多变量测试所需要的那么多流量，但是这种方法在不全局测试的前提下也不能保证一定能找到最优的因子组合。

## 多臂老虎机 Multi-armed Bandit (MAB)

为了利用好有限的流量和缩短实验时间，并在有限的周期内自动最小化机会成本，实验者可以使用多臂老虎机的方式。这种实验方法在开始实验后，根据不同对照组的表现情况，自动同时通过探索explore和利用exploit相结合的方式，尽快地找到最优的组合并把全部流量导向该组合。常见的算法如下：
1. $\varepsilon$-Greedy Algorithm
2. Upper Confidence Bounds
3. Thompson Sampling