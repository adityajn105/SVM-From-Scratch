# Implemeting SVM from scratch using Python

1. Refrence
	* [Youtube Link (watch 20-33)](https://youtu.be/mA5nwGoRAOo)

2. About SVM (General required for algo)
	* For all xi in training Data:
		 * ```	
		 	xi.w + b <= -1   if yi = -1 (belongs to -ve class)
		 	xi.w + b >= +1	if yi = +1 (belongs to +ve class)
		 				or
		 	 	__yi(xi.w+b) >= 1__
		 	```
	* for all support vectors(SV) (data points which decides margin)
		* ```
			xi.w+b = -1    here xi is -ve SV and yi is -1
			xi.w+b = +1    here xi is +ve SV and yi is +1
			```
	* For decision Boundary `yi(xi.w+b)=0` here xi belongs to point in decision boundary
	* Our Objective is to maximize Width W
		* `W = ((X+ - X-).w)/|w|`
		* or we can say minimize |w|
	* Once we have found optimized w and b using algorithm
		* `x.w+b = 1` is line passing through +ve support vectors
		* `x.w+b = -1` is line passing through -ve support vectors
		* `x.w+b = 0` is decision boundary
	* It is not necessary that support vector lines always pass through support vectors
	* It is a Convex Optimization problem and will always lead to a global minimum
	* This is Linear SVM means kernel is linear

3. Algorithm in Code (See code for better understanding)
	1. Start with random big value of w say(w0,w0) we will decrease it later
	2. Select step size as `w0*0.1` 
	3. A small value of b, we will increase it later
		* b will range from (-b0 < b < +b0, step = `step*b_multiple`)
		* This is also computational expensive. So select b0 wisely 
	4. We will check for points xi in dataset:
		* Check will for all transformation of w like (w0,w0), (-w0,w0), (w0,-w0), (-w0,-w0)
		* if not `yi(xi.w+b)>=1` for all points then break
		* Else find |w| and put it in dictionary as key and (w,b) as values 
	5. 
		* If w<=0 then current step have been completed and go to step 6
		* Else decrease w as (w0-step,w0-step) and continue with step 3
	6.  Do this step until step becomes `w0*0.001` because futher it will be point of expense
		* `step = step*0.1` 
		* go to step 3
	7. Select (w,b) which has min |w| form the dictionary 