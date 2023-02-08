1. Ambiguity
	1. Can cause issues in a language
	2. Arises when there exists multiple ways to parse a language
	3. Removing Ambiguity
		1. Add delimiters
			1. Modify grammars to add terminals of delimiters
		2. Add operator precedence
			1. Modify grammar
				1. Add additional non-terminals to indicate different levels of operator precedence
			2. Additional rules beyond grammar
		3. Define operator associativity
			1. Modify grammar
			2. Additional rules beyond grammar
2. Designing Grammars
	1. Use recursive productions to generate an arbitrary number of symbols
		1. $A\rightarrow xA\mid\varepsilon$         // Zero or more x's
		2. $A\rightarrow yA\mid y$         // One or more y's
	2. Use separated non-terminals to generated disjoint parts of a language an then combine in a production
		1. $a^*b^*$                   // a's followed by b's
		2. $S\rightarrow AB$           
		3. $A\rightarrow aA\mid\varepsilon$      // Zero or more a's
		4. $B\rightarrow bB\mid\varepsilon$      // Zero or more b's
	3. Matched Patterns
		1. To generate languages with matching, balanced, or related numbers of symbols, write productions which generate string from the middle
			1. Example 1:
				1. $(a^nb^n\mid n\geq0)$    // <i>n</i> a's followed by <i>n</i> b's
				2. $S\rightarrow aSb\mid\varepsilon$      
			2. Example 2:
				1. $(a^nb^{2n}\mid n\geq0)$  // <i>n</i> a's followed by 2<i>n</i> b's
				2. $S\rightarrow aSbb\mid\varepsilon$    
		2.  