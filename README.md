# 从零开始训练GPT2模型
==

## 1.项目描述:
---
本项目从头开始训练一个专门生成剧本的GPT2模型。使用精心收集的剧本语料进行训练，包括总语料大小约1.06M。最终模型能够生成戏剧对白和独白片段。

## 2.开始训练:
----

### (1)***模型配置***

在`train_drama.py`中定义了小型字符级GPT模型的超参数配置：

- `n_layer = 6`：Transformer层数，模型包含6层堆叠的Transformer块，适合小型数据集训练
- `n_head = 6`：多头注意力机制的头数，设置为6个独立的注意力头
- `n_embd = 384`：词嵌入维度，每个token的向量表示维度为384，相比标准GPT2更小巧
- `block_size = 256`：上下文窗口大小，模型能处理的最大序列长度为256个字符
- `batch_size = 64`：批处理大小设置为64，适合小型模型训练
- `dropout = 0.2`：Dropout率设置为0.2，防止过拟合
- `learning_rate = 1e-3`：学习率设置为0.001，对于小型网络可以设置得稍高一些
- `max_iters = 5000`：最大训练迭代次数为5000次
- `gradient_accumulation_steps = 1`：梯度累积步数为1，每次前向传播后立即更新参数

### (2)***模型训练***

使用剧本语料数据集训练小型GPT模型

......
iter 4720: loss 0.8297, time 30.23ms, mfu 12.50%
iter 4730: loss 0.8158, time 30.07ms, mfu 12.49%
iter 4740: loss 0.8280, time 30.11ms, mfu 12.48%
step 4750: train loss 0.6312, val loss 1.6901
iter 4750: loss 0.8094, time 4470.68ms, mfu 11.24%
iter 4760: loss 0.8222, time 31.06ms, mfu 11.31%
iter 4770: loss 0.7945, time 31.21ms, mfu 11.38%
iter 4780: loss 0.8098, time 30.05ms, mfu 11.48%
iter 4790: loss 0.8304, time 30.36ms, mfu 11.56%
iter 4800: loss 0.8200, time 31.03ms, mfu 11.60%
iter 4810: loss 0.8369, time 29.80ms, mfu 11.69%
iter 4820: loss 0.8217, time 30.39ms, mfu 11.75%
iter 4830: loss 0.8212, time 31.46ms, mfu 11.76%
iter 4840: loss 0.8218, time 30.92ms, mfu 11.79%
iter 4850: loss 0.8256, time 31.13ms, mfu 11.81%
iter 4860: loss 0.8241, time 31.01ms, mfu 11.83%
iter 4870: loss 0.8050, time 30.90ms, mfu 11.85%
iter 4880: loss 0.8258, time 31.37ms, mfu 11.85%
iter 4890: loss 0.8067, time 30.94ms, mfu 11.87%
iter 4900: loss 0.8017, time 20.63ms, mfu 12.49%
iter 4910: loss 0.8302, time 30.40ms, mfu 12.47%
iter 4920: loss 0.8036, time 30.72ms, mfu 12.43%
iter 4930: loss 0.8031, time 31.27ms, mfu 12.38%
iter 4940: loss 0.7949, time 29.56ms, mfu 12.40%
iter 4950: loss 0.8212, time 30.91ms, mfu 12.37%
iter 4960: loss 0.8320, time 30.87ms, mfu 12.34%
iter 4970: loss 0.7781, time 30.57ms, mfu 12.33%
iter 4980: loss 0.7922, time 30.64ms, mfu 12.31%
iter 4990: loss 0.8246, time 31.47ms, mfu 12.26%
step 5000: train loss 0.6158, val loss 1.7120
iter 5000: loss 0.8140, time 4468.96ms, mfu 11.04%

模型参数总量: 10,738,229 (~10.65M parameters)
训练数据集大小: ~1MB (约100万个字符)


训练过程中模型检查点将保存在`./model/`目录下，最终训练完成的模型文件为`ckpt.pt`。

### (3)***文本生成***

使用训练好的字符级莎士比亚模型进行文本生成：
```
================================================================================

Clown:
So, we will keep you that you have done with a man.

LUCIO:
You that should not be delay'd enough, you have a bazerous
and some further of mile displeasure: every contenting
in over-painted like your wanton like death, that
make him speak the spleen, and to see a dozen a lower:
the odd talk of all of your pity, we are doubt, and shortly poor
of his business; thrust for a sign of sheep-blowledge,
to fight a bodier, and so harried in hards. We are not shut best a
craved in-like hand: were 
---------------

Men pardon, marry how I was my master and see
On the prince with his house, where no success
Of my countrymation, castly, my instruction
And so under when my stead?

SICINIUS:
His poor matter:
He doth be respected:
Which is gracious that in Rome, who long'd
Her beauty against the walls of his self-honours,
To can make your seeming,--

BRUTUS:
He has a noble thief
That hath made of her some eyes and approachess
Being accompass'd the people, of some temperated
By this it of the good country.

SICI
---------------

Men that I both. Their fellows are under the corse, that
was of love back'd such a month wonth in some men
sound in men of high him; and here comes his goodly
cause him.

FLORIZEL:
A lord, to except the blame and liber
With golden native harmless courtest; so thou wert,
The palm of the springs of the earth,
Death to prove his ready brother; but that
The just tired that the people the blood
And can never the state that be present a thing
What with his blessing.

LEONTES:
Which the garland,
That's
---------------

The sleep of Buckingham, what a guard is the work
That can Clarence tell him that was now the
More than drunk? or my Lord Hastings, Grey'd now the Tower?

DUKE OF AUMERLE:
Why, how my man? she canst thou, my heart.

NORTHUMBERLAND:
Now flowers that thou corrupt of the harm, like the sanctuary.

DUKE OF YORK:
Bolingbroke, to blish it, if we were unsweeping it,
If you will want for us with the swallow, and sent me a brat,
And stand your Richard, to swear his bed.

DUKE OF YORK:
Well, I would have 
---------------

Be every beloved, her lord and very time
Are requite to the gallan and utmost haunts
From the noble Lord Angelo walls on his colour
To the deed pursuins of the second mile of his neck:
The poor good man is come to make his mother, not better more prophecy
To champion of the world good and seize of madness.

DUKE OF AUMERLE:
A biting as better than me, and not a brother,
In the deed, who hath sometime like her own soul,
But which he is pawn'd, as if any man he were less
That ever strength his for
---------------


MENENIUS:
He hath had not a sit, he does to go and me
say.

First Senator:
Ay, sir, no, he is not a man a man of alone,
that I have brought as he seeds, I have slept for you.

CORIOLANUS:
What, my mistress? or there's the most common should keep
From her vaint that bitter short, here between your hate,
Or an eason goodly to knowledge. You, till I not receive
For the common's death, which now you like my dream,
The hollow of my right divorce the search of his shop,
That his serforce will have pl
---------------

She will wear thee from me, spirit!
The way will say 'What, is my brother?'  thou wilt that I have:
And, I have guess'd some good time of York;
The dearer shall be a lerging king,
Not a lord like answer'd born.

RICHARD:
I, why, Tunsdom dost thou here ne'er be ruled with the arse?

NORTHUMBERLAND:
Good Catesby, do you me to this time.

DERBY:
What, art truly?
There was not the king with the gates of world?
But, that ten bloody foul thou apply wouldst care good,
His brother's so blood, and He is 
---------------

ladies here half hanged him as he in hand,
Anged a devising continuence, he streak not to see
The eye of the place of the jogs of place,
Were he drinken his true knownrightly service,
And obiding to him from the high of his affection.
But, how sorrow look upon him stand that exclaim'd by him;
And he wakes, as thou shalt hath come the hopeful woman:
Thou think'st the king we of the town, who thou here thou comest thee, that a
soldier more in the advantage of those shape,
Than a maid of woes, who 
---------------

GLOUCESTER:
Lord, good friend man; for your counsels, I know,
And bid his behalf well perfume so.
As he comes the clouds I scretch, so blest so.

GLOUCESTER:
Give me the man of his power: it is not the duke
Until your noble lord; where strength should rain a law ground,
Which he did make a piece of the king, and his father's broar,
And forget one that the lable king's countenance,
With purging too fruit on supply of this death,
Are not to our part. As we up. He the ruthless fellows,
And, this sa
---------------

He hath not settledge:
For we must not for that I have said to death
And see how they do not to part of my soul,
That is but ever-borne that a maid.

MARIANA:
Yet, marry, son:
I have done a world to the people; and who shall
Of our death is like a present in a little next present
To your money!

DUKE VINCENTIO:
It is now it is not concluded as his foul to the sea
And to be purposed to the trial third.

Clown:
Ay, sir. There is a thoughty has be.

MARCIUS:
You are glad, and make me, I am the perf

==========================================================================================
```

模型成功学习了剧作的语言风格，能够生成戏剧对白。
