CRISP-DM 框架

1.业务理解（Business Understanding）

-项目目标：识别对销量影响最大的关键因素（如评论数、折扣力度、评分等），构建决策树回归模型，预测亚马逊产品销量（sales）。
-预期业务价值：为卖家提供定价、促销和平台曝光策略优化依据；为电商平台提升推荐系统销量预测准确率。
-成功标准：模型在测试集上 R² > 0.6，且能清晰解释 Top 5 驱动因素。


2.数据理解（Data Understanding）

-数据来源：amazon_products.csv（约42,675条记录，15个字段）。
-初步探索：通过 df.info() 和 head() 查看数据结构、缺失值分布（sales、product_rating 等列有缺失）、变量类型（数值+类别）。


3.数据准备（Data Preparation）

删除 sales 为空的行（目标变量缺失样本无效）、对类别变量（is_best_seller、is_sponsored、product_category 等）进行 one-hot 编码、保留/计算衍生特征（如 discount_percentage）、数值缺失值采用中位数或均值填充（视情况）


4.建模（Modeling）

-模型选择：DecisionTreeRegressor
-流程：
      基线模型：默认参数决策树
      超参数调优：使用 GridSearchCV + 5折交叉验证，搜索 max_depth、min_samples_split、min_samples_leaf 等
      最佳模型：得到调优后的 best_tree


5.评估（Evaluation）

-方法：5折交叉验证（cross_validate / cross_val_predict）
-主要指标：MAE、RMSE、R²
-模型解释：特征重要性排序（pd.Series(feature_importances_)） + Top 20 条形图可视化
-核心洞察：销量最强驱动因素依次为 total_reviews（评论总数）、discount_percentage（折扣力度）、product_rating（评分）等，符合电商商业直觉。


6.部署（Deployment）-练习文件暂无部署~
