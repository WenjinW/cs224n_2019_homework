# CS 224n Assignment 2: word2vec

Name: Wenjin Wang

## (a) Answer:
All elements in $\vec{y}$ are equal with $0$, except $y_o=1$. So,
$$
-\sum_{w\in Vocab}y_w\log(\hat{y}_w)=-1\cdot \log(\hat{y}_o)
$$

## (b) Answer:
$$
\begin{align}
	\frac{\partial J}{\partial v_c}&=\frac{\partial -\log(\hat{y}_o)}{\partial v_c}=\frac{-1}{\hat{y}_o}\frac{\partial \frac{\exp(u_o^Tv_c)}{\sum_{w\in V}\exp(u_w^Tv_c)}}{\partial v_c}\\
	&=\frac{-1}{\hat{y}_o}[\frac{\exp(u_o^Tv_c)u_o}{\sum_{w\in V}\exp(u_w^Tv_c)}-\sum_{w\in V}\frac{\exp(u_o^Tv_c)\exp(u_w^Tv_c)u_w}{(\sum_{w\in V}\exp(u_w^Tv_c))^2}]\\
	&=-\frac{1}{\hat{y}_o}(\hat{y}_ou_o-\sum_{w\in V}\hat{y}_o\hat{y}_wu_w)=\sum_{w\in V}\hat{y}_wu_w-u_o\\
	&=U(\hat{y}-y)
\end{align}
$$

## (c) Answer:

If $w=o$
$$
\begin{align}
\frac{\partial J}{\partial u_o}&=-\frac{1}{\hat{y}_o}[\frac{\exp(u_o^Tv_c)v_c-\exp(u_o^Tv_c)\exp(u_o^Tv_c)v_c}{(\sum_{j\in V}\exp(u_j^Tv_c))^2}]=-\frac{\hat{y}_ov_c-\hat{y}_o\hat{y}_ov_c}{\hat{y}_o}\\
&=(\hat{y}_o-1)v_c=(\hat{y}_o-y_o)v_c
\end{align}
$$

if $w\neq o$
$$
\begin{align}
\frac{\partial J}{\partial u_w}&=-\frac{1}{\hat{y}_o}\frac{-\exp(u_o^Tv_c)\exp(u_wv_c)v_c}{(\sum_{j\in V}\exp(u_w^Tv_c))^2}=(-\frac{1}{\hat{y}_o})(-\hat{y}_o\hat{y}_wv_c)\\
&=\hat{y}_wv_c=(\hat{y}_w-y_w)v_c
\end{align}
$$
So, we have:
$$
\frac{\partial J}{\partial U}=v_c(\hat{y}-y)^T
$$

## (d) Answer:
We have:
$$
\sigma'(x_i)=\sigma(x_i)(1-\sigma(x_i))
$$
So:
$$
\frac{d\sigma(x)}{dx}=diag(\sigma(x)(1-\sigma(x)))
$$

## (e) Answer:
$$
\begin{align}
\frac{\partial J}{\partial v_c}&=-\frac{1}{\sigma(u_o^Tv_c)}\frac{\partial\sigma(u_o^Tv_c)}{\partial v_c}-\sum_{k=1}^K\frac{1}{\sigma(-u_k^Tv_c)}\frac{\partial\sigma(-u_k^Tv_c)}{\partial v_c}\\
&=-[1-\sigma(u_o^Tv_c)]u_o+\sum_{k=1}^K[1-\sigma(-u_k^Tv_c)]u_k\\
\frac{\partial J}{\partial u_o}&=-\frac{1}{\sigma(u_o^Tv_c)}\frac{\partial\sigma(u_o^Tv_c)}{\partial u_o}=-[1-\sigma(u_o^Tv_c)]v_c\\
\frac{\partial J}{\partial u_k}&=-\frac{1}{\sigma(-u_k^Tv_c)}\frac{\partial\sigma(-u_k^Tv_c)}{\partial u_k}=[1-\sigma(-u_k^Tv_c)]v_c
\end{align}
$$

In this loss function, we do not need to consider all words in corpus but only $K$ negative samples.

## (f) Answer:
$$
\begin{align}
\frac{\partial J_{skip-gram}(v_c,w_{t-m},\dots,w_{t+m},U)}{\partial U}&=\frac{\partial \sum_{\substack{-m\le j\le m \\ j\neq 0}}J(v_c,w_{t+j},U)}{\partial U}=\sum_{\substack{-m\le j\le m \\ j\neq 0}}\frac{\partial J(v_c,w_{t+j},U)}{\partial U}\\
\frac{\partial J_{skip-gram}(v_c,w_{t-m},\dots,w_{t+m},U)}{\partial v_c}&=\frac{\partial\sum_{\substack{-m\le j\le m \\ j\neq 0}}J(v_c,w_{t+j},U)}{\partial v_c}=\sum_{\substack{-m\le j\le m \\ j\neq 0}}\frac{\partial J(v_c,w_{t+j},U)}{\partial v_c}\\
\frac{\partial J_{skip-gram}(v_c,w_{t-m},\dots,w_{t+m},U)}{\partial v_w}&=0
\end{align}
$$


