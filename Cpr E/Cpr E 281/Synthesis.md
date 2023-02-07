1. ![[Boolean Algebra]]
2. Operator Precedence
	1. Similar to regular arithmetic, multiplication takes precedence over addition
	2. NOT > AND > OR
	3. Example:
		1. $S_1,S_2$
		2. $((0,0),(0,1),(1,1))=1$
		3. $(1,0)=0$
		4. $f(x_1,x_2)=\overline{x_1}+x_2$
	5. Canonical Sum-of-Products (SOP)
	6. Canonical Product-of-Sums (POS)
	7. Minimal-Cost Realization
		1. Optimization of a circuit 
	2. Minterms and Maxterms
		1. | Row Number | $x_1$ $x_2$ |         Minterm         |               Maxterm               |
		   | :--------: | :---------: | :---------------------: | :---------------------------------: |
		   |     0      |   0    0    | $m_0=\overline{x_1x_2}$ |            $M_0=x_1+x_2$            |
		   |     1      |   0    1    | $m_1=\overline{x_1}x_2$ |      $M_1=x_1+\overline{x_2}$       |
		   |     2      |   1    0    | $m_2=x_1\overline{x_2}$ |      $M_2=\overline{x_1}+x_2$       |
		   |     3      |   1    1    |      $m_3=x_1x_2$       | $M_3=\overline{x_1}+\overline{x_2}$ |
		
	2. 