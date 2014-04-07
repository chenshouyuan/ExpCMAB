adversarial cmab
================

# definitions
- $\tilde c_t(k) = \tilde l_t^T v_k$

# observations 
- outcomes of all arms $\{l_t(i), \forall  v_i(K_t) = 1\}$.


# construction of pseudo-observations $\tilde l_t$
- requirements
	+	$E[\tilde l_t] = l_t$
	+	$E[\tilde c_t(k)] = c_t(k)$ for all $k \in [K]$

-	construction
	$$\tilde l_t(i) = \begin{cases}
		\frac{l_t(i)}{\sum_{k=1}^K p_{t-1}(k) v_i(k)} & v_i(K_t) = 1,\\
		0 & v_i(K_t) = 0.
		\end{cases}
	$$

- properties
	$$ 
	\begin{aligned}
		E[\tilde l_t(i)] &= \left[\frac{l_t(i)}{\sum_{k=1}^K p_{t-1}(k) v_i(k)}\right] \sum_{k=1}^K p_{t-1}(k) v_i(k) \\
											&= l_t(i)
	\end{aligned} $$

- note
	$$ \sum_{k=1}^K p_{t-1}(k) v_i(k)	= E[v_i(K_t)].$$
	and hence
	$$
	\tilde l_t(i) = \frac{l_t(i) v_i(K_t)}{E[v_i(K_t)]}.
	$$

-	$E[v(K_t)v(K_t)^T]_{ij} = E[v_i(K_t) v_j(K_t)].$
	+ hence
	$$
	\begin{aligned}
	\tilde l_t^T E[v(K_t)v(K_t)^T] \tilde l_t &= 
		\sum_{ij} \tilde l_t(i)\tilde l_t(j) E[v(K_t)v(K_t)^T]_{ij}\\
		&=\sum_{ij} l_t(i)l_t(j)v_i(K_t)v_j(K_t) \frac{E[v_i(K_t)v_j(K_t)]}{E[v_i(K_t)]E[v_j(K_t)]}
	\end{aligned}
	$$
	

# proof: key steps
- cumulative pseudo-loss 
	$\tilde L_n(k) = \sum_{t=1}^n \tilde c_t(k)$.
- against the best 
	(@upper)
	$$
	\log\left(\frac{W_n}{W_0} \right) \ge -\eta \tilde L_n - \log(K).
	$$
- lower bound 
	(@lower-single)
	$$
	\begin{aligned}
	\log\left(\frac{W_t}{W_{t-1}} \right) & \le \frac{-\eta}{1-\gamma} \sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)+\frac{\eta\gamma}{1-\gamma}\sum_{k=1}^K \tilde c_t(k)\mu(k) + \frac{\eta^2}{1-\gamma}\sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)^2	
	\end{aligned}
	$$
	**proof missing**
- cumulative lower bound 
	(@lower)
	$$
	\log\left(\frac{W_n}{W_0}\right) \le 
	\frac{-\eta}{1-\gamma} \sum_{t=1}^n \sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)+\frac{\eta\gamma}{1-\gamma}\sum_{t=1}^n \sum_{k=1}^K \tilde c_t(k)\mu(k) + \frac{\eta^2}{1-\gamma}\sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)^2	
	$$
- combine (@lower) and (@upper)
	$$
	-\eta \tilde L_n - \log(K) \le 
	\frac{-\eta}{1-\gamma} \sum_{t=1}^n \sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)+\frac{\eta\gamma}{1-\gamma}\sum_{t=1}^n \sum_{k=1}^K \tilde c_t(k)\mu(k) + \frac{\eta^2}{1-\gamma}\sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)^2	
	$$
		
	rearrange,
	$$
	\frac{\eta}{1-\gamma} \sum_{t=1}^n \sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)
	\le 
	\eta \tilde L_n + \log(K)
	+\frac{\eta\gamma}{1-\gamma}\sum_{t=1}^n \sum_{k=1}^K \tilde c_t(k)\mu(k) + \frac{\eta^2}{1-\gamma}\sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)^2	
	$$

	divide by $\frac{\eta}{1-\gamma}$,
	$$
 	\sum_{t=1}^n \sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)
	\le 
	(1-\gamma) \tilde L_n + \frac{1-\gamma}{\eta}\log(K)
	+\gamma\sum_{t=1}^n \sum_{k=1}^K \tilde c_t(k)\mu(k) + \eta \sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)^2	
	$$
- expectations
	$$E[\sum_{t=1}^n \sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)] = E[\sum_{t=1}^n c_t(K_t)]$$
	**proof required**

- take expectation 
	$$
	\begin{aligned}
	E[\sum_{t=1}^n c_t(K_t)]
	&\le 
	(1-\gamma) E[\tilde L_n] + \frac{1-\gamma}{\eta}\log(K)
	+\gamma\sum_{t=1}^n \sum_{k=1}^K E[\tilde c_t(k)\mu(k)] + \eta \sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) E[\tilde c_t(k)^2]\\
	&=
	(1-\gamma) L_n + \frac{1-\gamma}{\eta}\log(K)
	+\gamma\sum_{t=1}^n \sum_{k=1}^K c_t(k)\mu(k) + \eta \sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) E[\tilde c_t(k)^2]\\	
	\end{aligned}
	$$
- bound the term $\sum_{t=1}^n\sum_{k=1}^K p_{t-1}(k) E[\tilde c_t(k)^2]$.
	+	by [comband], we have
		$$
			\sum_{k=1}^K p_{t-1}(k) \tilde c_t(k)^2 = \tilde l_t^T E[v(K_t)v(K_t)^T] \tilde l_t.
		$$

