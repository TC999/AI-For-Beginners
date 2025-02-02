# 深度强化学习

强化学习（RL）被认为是基本的机器学习范例之一，与监督学习和无监督学习并列。在监督学习中，我们依赖于具有已知结果的数据集，而强化学习则基于“边做边学”的原理。例如，当我们第一次玩电脑游戏时，即使不知道规则，我们也开始玩，通过玩游戏和调整行为的过程，我们很快就能提高自己的技能。

## [预讲座测验](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/122)

要进行RL，我们需要：

* 一个设定游戏规则的**环境**或**模拟器**。我们应该能够在模拟器中运行实验并观察结果。
* 一些**奖励函数**，用来表示我们的实验有多成功。对于学习玩电脑游戏来说，奖励就是我们的最终得分。根据奖励函数，我们应该能够调整我们的行为并改善我们的技能，以便下次我们玩得更好。强化学习与其他类型的机器学习的主要区别在于，在强化学习中，通常在游戏结束之前我们不知道是否获胜或失败。因此，我们无法判断某个动作是否好 - 我们只在游戏结束时获得奖励。

在强化学习过程中，我们通常进行多次实验。在每次实验中，我们需要在遵循已学到的最佳策略（**利用**）和探索新的可能状态（**探索**）之间取得平衡。

## OpenAI Gym

一个很好的强化学习工具是[OpenAI Gym](https://gym.openai.com/) - 一个**模拟环境**，可以模拟许多不同的环境，从Atari游戏到平衡杆背后的物理定律。它是训练强化学习算法最流行的模拟环境之一，由[OpenAI](https://openai.com/)维护。

> **注意**: 您可以在OpenAI Gym[这里](https://gym.openai.com/envs/#classic_control)查看所有可用的环境。## CartPole平衡

你可能已经见过现代的平衡设备，比如*Segway*或*Gyroscooters*。它们能够通过根据加速度计或陀螺仪的信号调整轮子来实现自动平衡。在本节中，我们将学习如何解决一个类似的问题 - 平衡一个杆子。这类似于马戏团表演者需要在手上平衡杆子的情况 - 但这种杆子平衡只发生在一维空间中。

平衡的简化版本被称为**CartPole**问题。在CartPole世界中，我们有一个水平滑块，可以向左或向右移动，目标是在滑块移动时在其顶部平衡一个垂直的杆子。

为了创建和使用这个环境，我们需要几行Python代码：

```python
import gym
env = gym.make("CartPole-v1")

env.reset()
done = False
total_reward = 0
while not done:
   env.render()
```
```python
action = env.action_space.sample()
observaton, reward, done, info = env.step(action)
total_reward += reward

print(f"Total reward: {total_reward}")
```

每个环境可以以完全相同的方式访问：
* `env.reset` 开始一个新的实验
* `env.step` 执行一步模拟。它接收来自**动作空间**的一个**动作**，并返回一个**观测值**（来自观测空间），以及一个奖励和一个终止标志。在上面的示例中，我们在每个步骤中执行一个随机动作，这就是为什么实验的寿命很短： 
 
![non-balancing cartpole](images/cartpole-nobalance.gif) 

RL算法的目标是训练一个模型 - 所谓的**策略**&pi; - 它将根据给定的状态返回动作。我们也可以考虑策略是概率的，例如对于任何状态 *s* 和动作 *a*，它将返回我们应该在状态 *s* 中采取 *a* 的概率 &pi;(*a*|*s*)。

## 策略梯度算法

最直观的建模策略的方法是创建一个神经网络，以状态作为输入，并返回相应的动作（或者更准确地说是所有动作的概率）。在某种意义上，这类似于一个常规的分类任务，但有一个重大的区别 - 我们事先不知道在每个步骤中应该采取哪些动作。这里的想法是估计这些概率。我们构建了一个**累积奖励**的向量，显示了实验每一步的总奖励。我们还通过将早期奖励乘以某个系数&gamma;=0.99来应用**奖励折现**，以减少早期奖励的作用。然后，我们强化那些产生较大奖励的实验路径上的步骤。

> 在[示例笔记本](CartPole-RL-TF.ipynb)中了解有关策略梯度算法的更多信息并看它的实际应用。

## 演员-评论家算法

策略梯度方法的改进版本称为**演员-评论家**。其主要思想是神经网络将被训练返回两个东西：

* 策略，确定要采取的动作。这部分称为**演员*** 该状态下我们可以期望获得的总奖励估计 - 这部分称为**批评家**。

从某种意义上讲，这种架构类似于[GAN](../../4-计算机视觉/10-GANs/README.md)，我们有两个网络相互对抗训练。在演员-批评家模型中，演员提出我们需要采取的动作，而批评家尝试批评并估计结果。然而，我们的目标是同时训练这些网络。

因为我们知道实际的累积奖励和批评家在实验期间返回的结果，所以相对容易构建一个损失函数来最小化它们之间的差异。这将给出**批评家损失**。我们可以通过使用与策略梯度算法相同的方法来计算**演员损失**。

运行其中一种算法后，我们可以期望我们的CartPole表现如下：

![均衡的CartPole](images/cartpole-balance.gif)## ✍️ 练习：策略梯度和Actor-Critic强化学习

在以下笔记本中继续学习：

* [使用TensorFlow的强化学习](CartPole-RL-TF.ipynb)
* [使用PyTorch的强化学习](CartPole-RL-PyTorch.ipynb)

## 其他强化学习任务

强化学习现在是一个快速发展的研究领域。一些有趣的强化学习示例包括：* 训练一台计算机玩**Atari游戏**。这个问题的挑战在于，我们没有简单的以矢量表示的简单状态，而是一个屏幕截图-我们需要使用CNN将此屏幕图像转换为特征向量，或提取奖励信息。Atari游戏在Gym里可用。
* 训练一台计算机玩棋盘游戏，如国际象棋和围棋。最近，最先进的程序如**Alpha Zero**是通过两个互相对战并在每一步中改进的代理进行训练的。
* 在工业领域中，RL被用于从模拟中创建控制系统。一个名为[Bonsai](https://azure.microsoft.com/services/project-bonsai/?WT.mc_id=academic-77998-cacaste)的服务专门为此设计。

## 结论

我们现在已经学会了如何训练代理程序以达到良好的结果，只需要为它们提供定义游戏期望状态的奖励函数，并给予它们智能探索搜索空间的机会。我们成功尝试了两种算法，并在相对短的时间内取得了良好的结果。然而，这只是你进入RL之旅的开始，如果想深入探讨，你应该考虑参加另外的课程。

## 🚀 挑战

## [课后测验](https://red-field-0a6ddfd03.1.azurestaticapps.net/quiz/222)

## 回顾与自学

在我们的[机器学习入门课程](https://github.com/microsoft/ML-For-Beginners/blob/main/8-Reinforcement/README.md)中了解更多关于经典强化学习的知识。

观看这个[很棒的视频](https://www.youtube.com/watch?v=qv6UVOQ0F44)，讲述了计算机如何学习玩超级马里奥。## 任务：[训练山地车](lab/README.md)

在本任务中，您的目标是训练不同的Gym环境 - [Mountain Car](https://www.gymlibrary.ml/environments/classic_control/mountain_car/)。