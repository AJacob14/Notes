1. In AST classes, every class implements a method that accept that takes an object of type Visitor as a parameter and invokes method visit on that object
2. Visitor Interface
   ```Java
   interface Visitor<T>{
	   T visit(NumExp e);
	   T visit(AddExp e);
	   T visit(MultExp e);
	   T visit(SubExp e);
	   T visit(DivExp e);
	   T visit(Program p);
   }
```
3. 