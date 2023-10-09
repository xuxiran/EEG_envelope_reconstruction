# EEG_envelope_reconstruction
Attention: all the code would be released after paper publication
注意：代码将在论文正式发表后释放

English
This is the code of project won the "Challenge of Auditory-EEG".You could get the original data and final rank in https://challenge.xfyun.cn/topic/info?type=auditory-eeg
![image](https://github.com/xuxiran/EEG_envelope_reconstruction/assets/48015859/cb8d37c7-7e48-4085-930f-903ea14eddd3)

This is a brief introduction to the solution for the project. Firstly, we will introduce the testing related code, followed by the training related code.
The Python environment used is 3.9, and the version of Torch used is 1.13.0.

Solution: An improved model similar to VAIIL has been proposed. The specific logic will be made public after the publication of the paper. 
You only need to run 'train.py' to reproduce the training process. 'train.py' will call 'EEG_Dataset.py' to convert the EEG data into a Dataset. 
The model is in 'newmodel.py'. All model training parameters are saved in 'config.py'.

Testing related code: You only need to run test.py. 
We assume that there are two files, 'auditory-eeg-test-dataset' and 'test_labels', under 'project/xfdata'. 
If the file path is incorrect, it may result in inference failure. You can manually modify the file path in 'run test.py' or contact me to resubmit the code. 
After running 'test.py', you will obtain the predicted EEG envelopes for all subjects in 'project/prediction_result/'. 
If test_labels are the same as those used in the competition, you can obtain a score of 0.18508. 
We are sorry that due to some mistakes, the model with a score of 0.18519 was overwritten. 
However, as we provide the training code, you can try different random seeds and perhaps obtain results higher than 0.18519.

Training related code: You only need to run train.py. 
We did not use any data augmentation because it may overfit the test set. 
However, we found that the random seed has a significant impact on the final result. 
Initially, we thought it was due to model differences and modified the model to obtain different results. 
However, the huge fluctuations in score prompted us to conduct ablation analysis. 
We fixed the model architecture and only modified the random seed. However, the trained models still have significant differences. 
As a result, considering that we were allowed to submit three times a day, we tried different random seeds with same models and submitted nine times. 
The scores for these nine submissions were: 0.18249, 0.18508, 0.18519, 0.17783, 0.18054, 0.17861, 0.17783, 0.17858, and 0.17715. 
It is worth noting that all of these scores are higher than the second-place result (0.17657), indicating that our model is significantly superior to the current SOTA. 
However, it can also be concluded that the final score will depend on the design of the random seed. 
This is actually a common phenomenon in machine learning.

In addition, it is also worth mentioning that the current SOTA (VIAAL) also has similar characteristics. 
Although we cannot submit VIAAL, on the local validation set, the random seed also has a significant impact on the result of validation set. 
We will continue to investigate this in the future. Pilot experiment suggests that the difference in the final result may be due to the dataset partitioning 
and model initialization, which is a common reason in other machine learning fields.

Closing Remarks: We apologize for the limited time available to provide a more complete report due to the deadline of ICASSP paper submission
and the need to submit other work. The complete paper for this project will be written after the ICASSP paper submission deadline, 
and all code will be made available on Github after the paper is completed and submitted on arxiv.

中文：
这是我们在算法挑战赛：听觉脑电（Auditory-EEG）挑战赛的实现方案（最终排名第一）。在网址https://challenge.xfyun.cn/topic/info?type=auditory-eeg，你将能看到比赛简介、数据以及最终排行榜。
![image](https://github.com/xuxiran/EEG_envelope_reconstruction/assets/48015859/8bf77507-6909-47ab-a1eb-6ce806feac9b)

这是project的解决方案简介。首先我们将介绍测试相关代码，然后介绍训练相关代码。python环境为3.9，torch版本为1.13.0

解决方案：一种类似于VAIIL的改进模型被提出。具体的逻辑将在论文发表后公开。您只需要运行train.py就可以复现训练流程。
train.py将调用EEG_Dataset.py，从而将脑电数据变为Dataset。模型在"newmodel.py"中。
模型训练所有参数保存在config.py中。

测试相关代码：您只需要运行test.py即可
我们假设'project/xfdata' 下存在'auditory-eeg-test-dataset'和'test_labels'两个文件。
如果文件路径错误，会导致无法推理。请手动修改文件路径，或者也可以联系我重新提交代码。
test.py运行后，您将在'project/prediction_result/'下获得所有被试的预测脑电包络。
如果test_labels和比赛时一样，您可以获得0.18508的评分。
我们很抱歉由于一些失误，获得0.18519的评分的模型被覆盖了。
但是由于我们提供了训练代码，您可以多尝试一些随机种子，也许能获得高于0.18519的结果。

训练相关代码：您只需要运行train.py即可
我们没有对数据采用任何数据增广。这是因为数据增广有过拟合测试集的嫌疑。
但是我们发现随机种子对最终结果将产生较大的影响。
一开始我们也以为是模型的差异，并且修改模型尝试获得不同结果。但是评分的巨大波动让我们开始消融分析。
我们固定了模型架构，并且只修改随机种子。然而训练出的模型仍然有较大差异。
简单的说，由于我们被允许每天提交三次，类似的模型我们尝试了不同的随机种子，并提交了9次。
这9次的评分分别是：0.18249, 0.18508, 0.18519, 0.17783. 0.18054, 0.17861, 0.17783, 0.17858 和 0.17715
值得注意的是，这9个评分都高于第二名的结果（0.17657），因此我们可以得出结论，我们的模型的确是显著优于当前SOTA的。
但是也可以确定，最终评分将依赖于随机种子的设计。这一点其实在机器学习中较为常见。

另外也需要提及一点，当前SOTA(VIAAL)也会有类似的特点。
虽然我们没有办法提交VIAAL，但是在本地验证集上，随机种子对验证集结果也会产生较大的影响。
这一点我们将在后期继续研究。初期分析，可能是由于数据集划分以及模型初始化导致了最终结果的差异，这也是其它机器学习领域较为常见的原因。

写在最后：我们很抱歉由于ICASSP的临近并且我们有其它工作需要投稿，很难抽出时间给出一份更加完整的报告。
这项工作完整的论文将在ICASSP投稿结束后开始撰写，在论文撰写完成并投稿至arxiv后，所有代码将开源至Github。
