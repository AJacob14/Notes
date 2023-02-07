1. Pseudocode for gradient descent approach
	1. ```
	   while \nabla J(w) > \theta do
		   w_{k+1} := w_k - \rho(k)\nabla J(w)
		   k := k + 1
		end while