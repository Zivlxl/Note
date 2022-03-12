#### TAIR: Testability Analysis by Implication Reasoning

##### 介绍

TAIR是基于COP的一个改进可测性方法，能够在不显著增加运行时间的情况下给出更接近真实（exact）可测性（testability）的结果。另外，TAIR可以将冗余故障的可测性直接设置成0。

##### 背景、定义

###### cop

cop（controllability/observability probability）代表节点的可控制性和可观测性的可能性。

单点n的v-controllability是使节点n的值为v的可能性-p(n=v)，多点的可能性为多个节点的值设置成指定的v1-vk, p(n0=v0, …，nk=vk)，如果多个节点结构上相互独立p(n0 = v0，n1 = v1，……，nk = vk) 

= p(n0 = v0) *p(n1 = v1)……*p(nk = vk):

