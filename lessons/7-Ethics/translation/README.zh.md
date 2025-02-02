# 道德和负责任的人工智能

你即将完成这门课程，我希望到现在你已经清楚地看到人工智能是基于一些正式的数学方法，这些方法允许我们在数据中找到关系并训练模型来复制人类行为的某些方面。在历史的这个阶段，我们认为人工智能是一种非常强大的工具，可以从数据中提取模式，并将这些模式应用于解决新的问题。

## [课前测验](https://white-water-09ec41f0f.azurestaticapps.net/quiz/5/)

然而，在科幻小说中，我们经常看到人工智能对人类构成了危险。通常这些故事都以某种人工智能反叛为中心，当人工智能决定对抗人类时。这意味着人工智能具有某种情感或者可以做出开发者未曾预料到的决策。

我们在这门课程中学到的人工智能只不过是大矩阵运算而已。它是一个非常强大的工具，可以帮助我们解决问题，就像其他强大的工具一样，它可以被用于善良和恶意的目的。重要的是，它可以被*滥用*。## 负责任 AI 的原则

为了避免 AI 的意外或故意滥用，微软确定了负责任 AI 的重要原则。以下概念支撑着这些原则：

- **公正性** 与 *模型偏见* 问题有关。使用具有偏见的数据进行训练可能导致模型偏见。例如，当我们试图预测一个人获得软件开发工作的可能性时，模型很可能更加偏向男性，因为训练数据集可能存在男性偏向的问题。我们需要仔细平衡训练数据，并调查模型以避免偏见，并确保模型考虑到更相关的特征。
- **可靠性和安全性**。由于其本质的缘故，AI 模型可能会犯错。神经网络返回概率，我们在做决策时需要考虑到这一点。每个模型都有一些准确率和召回率，我们需要了解这些以防止错误建议可能导致的伤害。
- **隐私和安全** 对于 AI 有一些特定影响。例如，当我们使用某些数据来训练模型时，这些数据被某种方式"整合"到了模型中。一方面，这增加了安全性和隐私性，另一方面 - 我们需要记住模型是基于哪些数据进行训练的。
- **包容性** 意味着我们构建 AI 的目的不是为了取代人类，而是为了增强人类能力，使我们的工作更具创造力。这也与公正性有关，因为在处理少数群体时，我们收集的大多数数据集很可能存在偏见，我们需要确保这些群体被包含在内，并且 AI 对其进行了正确处理。
- **透明度** 包括确保我们始终清楚地使用了 AI。此外，在可能的情况下，我们希望使用可解释的 AI 系统。
- **责任** 当 AI 模型做出某些决策时，并不总是清楚谁负责这些决定。我们需要确保我们理解 AI 决策的责任在哪里。大多数情况下，我们希望将人类纳入到做出重要决策的过程中，以便真正的人类承担责任。## 负责任人工智能的工具

Microsoft开发了[负责任AI工具箱](https://github.com/microsoft/responsible-ai-toolbox)，其中包含一组工具：

* 解释性仪表板（InterpretML）
* 公平性仪表板（FairLearn）
* 错误分析仪表板
* 负责任AI仪表板，其中包括- EconML - 用于因果分析的工具，专注于假设性问题
- DiCE - 用于反事实分析的工具，可以看到需要更改哪些特征以影响模型的决策

有关AI伦理的更多信息，请访问[此课程](https://github.com/microsoft/ML-For-Beginners/tree/main/1-Introduction/3-fairness?WT.mc_id=academic-77998-cacaste)，其中包括作业。

## 复习与自学

参考[此学习路径](https://docs.microsoft.com/learn/modules/responsible-ai-principles/?WT.mc_id=academic-77998-cacaste)了解更多关于负责任的AI的知识。

## [讲座后的测验](https://white-water-09ec41f0f.azurestaticapps.net/quiz/6/)