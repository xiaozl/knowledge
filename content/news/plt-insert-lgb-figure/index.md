---
# type: docs 
title: Matplot画图Firuge中插入Lgb等其他的Axes值
date: 2022-11-07T15:53:21+08:00
featured: true
draft: false
comment: false
toc: true
reward: true
pinned: true #置顶内容
carousel: false
series:
categories: []
tags:
 - Python
images: []
---

  Matplot画图时，需要把其他算法生成的图插入到plt的Figure中进行替换
  
----
>直接上代码

~~~~python
# Importing library
import matplotlib.pyplot as plt
import lightgbm as lgb
import numpy as np

x_train = np.random.random((1000, 10))
y_train = np.random.rand(1000) > 0.5
x_test = np.random.random((100, 10))
y_test = np.random.randn(100) > 0.5
 
# 导入到lightgbm矩阵
lgb_train = lgb.Dataset(x_train, y_train)
lgb_test = lgb.Dataset(x_test, y_test, reference=lgb_train)
 
# 设置参数
params = {
    'num_leaves': 5,
    'metric': ('auc', 'logloss'),  # 可以设置多个评价指标
    'verbose': 0
}

evals_result = {}  # 记录训练结果所用
 
print('开始训练...')
# train
gbm = lgb.train(params,
                lgb_train,
                num_boost_round=100,
                valid_sets=[lgb_train, lgb_test],
                evals_result=evals_result,  # 非常重要的参数,一定要明确设置,输出的结果是上面一个参数valid_sets配置的值
                verbose_eval=10)

#plt 里面定义的figure
fig = plt.figure()
#lgb 生成的ax内容
ax = lgb.plot_importance(gbm, max_num_features=10)
ax.set_title("Featurertances 20")

#关键的两个步骤,把ax里面的内容替换到figure里面
ax.figure = fig
# fig.axes.append(ax) #尝试后此内容无效
fig.add_axes(ax)


fig.savefig('1.png')   # save the figure to file
fig.canvas.draw()

~~~~

代码运行后可以正常把相关内容展示出来

>网上找的其他的代码信息

~~~python
def move_axes(ax, fig, subplot_spec=111):
      """Move an Axes object from a figure to a new pyplot managed Figure in
      the specified subplot."""

      # get a reference to the old figure context so we can release it
      old_fig = ax.figure

      # remove the Axes from it's original Figure context
      ax.remove()

      # set the pointer from the Axes to the new figure
      ax.figure = fig

      # add the Axes to the registry of axes for the figure
      fig.axes.append(ax)
      # twice, I don't know why...
      fig.add_axes(ax)

      # then to actually show the Axes in the new figure we have to make
      # a subplot with the positions etc for the Axes to go, so make a
      # subplot which will have a dummy Axes
      dummy_ax = fig.add_subplot(subplot_spec)

      # then copy the relevant data from the dummy to the ax
      ax.set_position(dummy_ax.get_position())

      # then remove the dummy
      dummy_ax.remove()

      # close the figure the original axis was bound to
      plt.close(old_fig)
~~~

