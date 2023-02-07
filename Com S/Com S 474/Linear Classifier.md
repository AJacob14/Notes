1. Vectors
	1. $\hat{v}=[v_0,v_1,v_2]$
	2. Generalized form of the dot product of two 1D vectors:
		1. $\sum_ix_iy_i=x_1y_1+x_2y_2+\dots$
	3. Feature Vector
		1. An orders list of numerical properties of an observed phenomena
		2. I.e., a vector where the elements have real-world meaning
2. Matrix
	1. Examples
		1. Creating matrix from two vectors
			1. $V_A=[2,3,5]$
			2. $V_B=[4,2,1]$
			3. $M_{AB}=\begin{pmatrix}2&4\\3&2\\5&1\end{pmatrix}$
		2. Creating matrix from system of equation
			  1. $\begin{cases}a_1x+b_1y=c_1\\a_2x+b_2y=c2\end{cases}$
			  2. $\begin{pmatrix}a_1&b_1\\a_2&b_2\end{pmatrix}\begin{pmatrix}x\\y\end{pmatrix}=\begin{pmatrix}c_1\\c_2\end{pmatrix}$
	2. Convention
		1. Vectors are column-vectors by default
3. Tensor
	1. Matrices and vectors are special cases of tensors
4. Hyperplane
	1. Line going through the x- and y-axis
		1. Equation: $x_1w_1+x_2w_2-w_1w_2=0$
		2. Matrix Form: $\begin{pmatrix}x_1&x_2&1\end{pmatrix}\begin{pmatrix}w_1\\w_2\\-w_1w_2\end{pmatrix}=\begin{pmatrix}x_1\\x_2\\1\end{pmatrix}^T\begin{pmatrix}w_1\\w_2\\-w_1w_2\end{pmatrix}=0$
		3. Let: 
			1. $x=\begin{pmatrix}x_1\\x_2\\1\end{pmatrix}$
			2. $w=\begin{pmatrix}w_1\\w_2\\-w_1w_2\end{pmatrix}$
			3. $x_1$ and $x_2$ are two **feature values** comprising the feature. 1 is the **augmented** for the bias $-w_1w_2$
			4. Equation is rewritten in matrix form: $x^Tw=x^T\cdot w$
			5. Since $x$ and $w$ are both vectors, $x^Tw=w^Tx$
		6. Expand to D-dimension
			1. $x=\begin{pmatrix}x_1\\x_2\\\vdots\\x_D\\1\end{pmatrix}$
			2. $w=\begin{pmatrix}w_1\\w_2\\\vdots\\w_D\\-w_1w_2\end{pmatrix}$
			3. Then $x^T\cdot w=0$, denoted as the *hyperplane* in $\mathbb{R}^n$
5. Binary Linear Classifier
	1. A binary linear classifier is a function $\hat{f}(x)=sgn(w^Tx)\in\{-1,0,1\}$ where $sgn$ is the sign function
	2. A properly trained binary linear classifier should hold that $$\begin{cases}w^Tx>0&\forall x\in C_1\\w^Tx<0&\forall x\in C_2\end{cases}$$ where $C_1$ and $C_2$ are the two classes.
	3. Convention
		1. Fit - Training Data
		2. Predict - Output of trained function
6. Normalized Feature Vector
	2. Simplest Way to Find $W$
		1. Let the training set be $\{(4,+1),(5,+1),(1,-1),(2,-1)\}$
		2. Augmented feature vectors are $x_1=(4,1)^T,x_2=(5,1)^T,x_3=(1,1)^T,x_4=(2,1)^T$
		3. Let $w^T=(w_1,w_2)$. In the training process, we establish 4 inequalities: $$\begin{cases}4w_1+w_2&>0\\5w_1+w_2&>0\\w_1+w_2&<0\\2w_1+w_2&<0\end{cases}$$
		4. Many $w_1$ and $w_2$ exist that satisfy the inequality, but how to find the best pair of values?
		5. Euclidian Distance
			1. $(y_1-\hat{y_1})^2+(y_2-\hat{y_2})^2+\dots$
		6. Gradient
			1. Recall: the partial derivative of a multivariate function is a vector called the gradient, representing the derivatives of a function on different directions
			2. For example, let $f(x)=x_1^2+4x_1+2x_1x_2+2x_2^2+2x_2+14$. $f$ maps a vector $x=(x_1,x_2)^T$ to a scalar.
			3. Then we have $$\nabla f=\frac{\partial f}{\partial x}=\begin{pmatrix}\frac{\partial f}{\partial x_1}\\\frac{\partial f}{\partial x_2}\end{pmatrix}=\begin{pmatrix}2x_1+2x_2+4\\4x_2+2x_1+2\end{pmatrix}$$
			4. Gradient is a special case of *Jacobian matrix* (see also: *Hessian matrix* for second-order partial derivatives)
			5. A *critical point* or a *stationary point* is reached where the derivative is zero on any direction.
				1. a local extremum (max or min)
				2. saddle point
			3. if a function is convex, a local maximum/minimum is the *global maximum/minimum*
		7. Zero-Gradient
			1. Two steps:
				1. Define a cost function to be minimized
				2. Choose an algorithm to minimize the cost function with
			2. Sum of error square
				1. $J(w)=\sum_{i=1}^N(w^Tx_i-y_i)^2=\sum_{i=1}^N(x_i^Tw-y_i)^2$
				2. Where $x_i$ is the i-th sample (out of $N$ samples), $y_i$ is the corresponding label, and $w^TX$ is the prediction
			3. Minimizing $J(w)$ means: $\frac{\partial J(w)}{\partial w}=2\sum_{i=1}^Nx_i(x_i^Tw-y_i)=(0,\dots,0)^T$
			4. Hence, $\sum_{i=1}^Nx_ix_i^Tw=\sum_{i=1}^Nx_iy_i$
			5. The sum of a column vector multiplied with a row vector produces a matrix.
				1. $$\sum_{i=1}^Nx_ix_i^T=\begin{pmatrix}\mid&\mid&&\mid\\x_1&x_2&\cdots&x_N\\\mid&\mid&&\mid\end{pmatrix}\begin{pmatrix}\textemdash&x_1^T&\textemdash\\\textemdash&x_2^T&\textemdash\\&\vdots&\\\textemdash&x_N^T&\textemdash\end{pmatrix}=\mathbb{X}^T\mathbb{X}$$
				2. $$\sum_{i=1}^Nx_iy_i=\begin{pmatrix}\mid&\mid&&\mid\\x_1&x_2&\cdots&x_N\\\mid&\mid&&\mid\end{pmatrix}\begin{pmatrix}x_1^T\\x_2^T\\\vdots\\x_N^T\end{pmatrix}=\mathbb{X}^Ty$$
				3. $\mathbb{X}^T\mathbb{X}w=\mathbb{X}^Ty$
				4. $(\mathbb{X}^T\mathbb{X})^{-1}\mathbb{X}^T\mathbb{X}w=(\mathbb{X}^T\mathbb{X})^{-1}\mathbb{X}y$
				5. $w=(\mathbb{X}^T\mathbb{X})^{-1}\mathbb{X}^Ty$
		6. Gradient Descent Approach
			1. Algorithm 1: pseudocode for gradient descent approach
				1. **Input**: an initial $w$, stop criterion $\theta$, a learning rate function $p(\cdot)$, iteration step $k=0$
				2. ![[Gradient Descent]]
				3. 