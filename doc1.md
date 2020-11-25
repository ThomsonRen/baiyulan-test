---
id: doc1
title: Style Guide
sidebar_label: Style Guide
slug: /
---

Check the [documentation](https://docusaurus.io) for how to use Docusaurus.

Lift($L$) can be determined by Lift Coefficient ($C_L$) like the following
equation.

$$
L = \frac{1}{2} \rho v^2 S C_L
$$

# 熵权法概览

## 学科分属

熵权法隶属于应用数学中的信息论学科分支。

## 历史发展

   熵最先由Claude Shannon引入信息论，目前已经在工程技术、社会经济等领域得到了非常广泛的应用。照信息论基本原理的解释，信息是系统有序程度的一个度量，熵是系统无序程度的一个度量；如果指标的信息熵越小，该指标提供的信息量越大，在综合评价中所起作用理当越大，权重就应该越高。



# 熵权法模型介绍

## 定义介绍

熵权法的基本思路是根据指标变异性的大小来确定客观权重。一般来说，若某个指标的信息熵$E_j$越小，表明指标值得变异程度越大，提供的信息量越多，在综合评价中所能起到的作用也越大，其权重也就越大。相反，某个指标的信息熵$E_j$越大，表明指标值得变异程度越小，提供的信息量也越少，在综合评价中所起到的作用也越小，其权重也就越小。 



## 熵权法赋权步骤

### 数据标准化

将各个指标的数据进行标准化处理。假设给定了$k$个指标$X_1$,$X_2$,...$X_k$,其中$X_i={x_1,x_2,...x_n}$。假设对各指标数据标准化后的值为$Y_1,Y_2,...Y_k$,那么
$$
Y_{ij}=\dfrac{X_{ij}-\min(X_i)}{ \max (X_j)-\min(X_i)}
$$

### 求各指标的信息熵

根据信息论中信息熵的定义，一组数据的信息熵
$$
E_j=- \ln (n)^{-1} \sum_{i=1}^np_{ij} \ln p_{ij}
$$

其中$P_{ij} = Y_{ij} / \sum_{i=1}^n Y_{ij}$,如果$P_{ij}=0$,则定义$\lim_{p_{ij}\to 0} p_{ij} \ln p_{ij} = 0$

### 确定各指标的权重

根据信息论中信息熵的计算公式，计算出各个指标的信息熵为$E_1,E_2,...,E_k$。

通过信息熵计算各指标的权重：$$W_i =\dfrac{1-E_i}{k-\sum E_i}(i=1,2,...,k)$$



# 代码实现



```matlab
function weights = EntropyWeight(R)
%% 熵权法求指标权重,R为输入矩阵,返回权重向量weights

[rows,cols]=size(R);   % 输入矩阵的大小,rows为对象个数，cols为指标个数
k=1/log(rows);         % 求k

f=zeros(rows,cols);    % 初始化fij
sumBycols=sum(R,1);    % 输入矩阵的每一列之和(结果为一个1*cols的行向量)
% 计算fij
for i=1:rows
    for j=1:cols
        f(i,j)=R(i,j)./sumBycols(1,j);
    end
end

lnfij=zeros(rows,cols);  % 初始化lnfij
% 计算lnfij
for i=1:rows
    for j=1:cols
        if f(i,j)==0            lnfij(i,j)=0;
        else
            lnfij(i,j)=log(f(i,j));
        end
    end
end

Hj=-k*(sum(f.*lnfij,1)); % 计算熵值Hj
weights=(1-Hj)/(cols-sum(Hj));
end
```




这是我在2020-11-24晚上的测试项目

```{python}
import numpy as np
for i in range(10):
    print('hello world')
```

```{matlab}
load data.mat
clc;clear;close all;
x = 0;
for i=1:10
   x = x + 1;
end
fprintf('hello world')
```

## Mauris In Code

```
Mauris vestibulum ullamcorper nibh, ut semper purus pulvinar ut. Donec volutpat orci sit amet mauris malesuada, non pulvinar augue aliquam. Vestibulum ultricies at urna ut suscipit. Morbi iaculis, erat at imperdiet semper, ipsum nulla sodales erat, eget tincidunt justo dui quis justo. Pellentesque dictum bibendum diam at aliquet. Sed pulvinar, dolor quis finibus ornare, eros odio facilisis erat, eu rhoncus nunc dui sed ex. Nunc gravida dui massa, sed ornare arcu tincidunt sit amet. Maecenas efficitur sapien neque, a laoreet libero feugiat ut.
```

## Nulla

Nulla facilisi. Maecenas sodales nec purus eget posuere. Sed sapien quam, pretium a risus in, porttitor dapibus erat. Sed sit amet fringilla ipsum, eget iaculis augue. Integer sollicitudin tortor quis ultricies aliquam. Suspendisse fringilla nunc in tellus cursus, at placerat tellus scelerisque. Sed tempus elit a sollicitudin rhoncus. Nulla facilisi. Morbi nec dolor dolor. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Cras et aliquet lectus. Pellentesque sit amet eros nisi. Quisque ac sapien in sapien congue accumsan. Nullam in posuere ante. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Proin lacinia leo a nibh fringilla pharetra.

## Orci

Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Proin venenatis lectus dui, vel ultrices ante bibendum hendrerit. Aenean egestas feugiat dui id hendrerit. Orci varius natoque penatibus et magnis dis parturient montes, nascetur ridiculus mus. Curabitur in tellus laoreet, eleifend nunc id, viverra leo. Proin vulputate non dolor vel vulputate. Curabitur pretium lobortis felis, sit amet finibus lorem suscipit ut. Sed non mollis risus. Duis sagittis, mi in euismod tincidunt, nunc mauris vestibulum urna, at euismod est elit quis erat. Phasellus accumsan vitae neque eu placerat. In elementum arcu nec tellus imperdiet, eget maximus nulla sodales. Curabitur eu sapien eget nisl sodales fermentum.

# Phasellus

Phasellus pulvinar ex id commodo imperdiet. Praesent odio nibh, sollicitudin sit amet faucibus id, placerat at metus. Donec vitae eros vitae tortor hendrerit finibus. Interdum et malesuada fames ac ante ipsum primis in faucibus. Quisque vitae purus dolor. Duis suscipit ac nulla et finibus. Phasellus ac sem sed dui dictum gravida. Phasellus eleifend vestibulum facilisis. Integer pharetra nec enim vitae mattis. Duis auctor, lectus quis condimentum bibendum, nunc dolor aliquam massa, id bibendum orci velit quis magna. Ut volutpat nulla nunc, sed interdum magna condimentum non. Sed urna metus, scelerisque vitae consectetur a, feugiat quis magna. Donec dignissim ornare nisl, eget tempor risus malesuada quis.
