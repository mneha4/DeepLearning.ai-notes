####-	**Normalisation**:
>		If feature range is different, for example: x1 ranges from (0,1) and x2 from (1,100000) then  you should normalize your dataset.
>		Normalization helps in reaching minimum of  cost function easily (less training steps).
>	
####-	**Mini Batch Gradient Descent**
>		mini-batch size = m, Batch Gradient Descent (too long per iteration)
>		mini-batch size = 1, Stochastic Gradient Descent
	
####-	**Stochastic Gradient Descent**
>		Very noisy
>		Use low learning rate
>		Very slow
>		Loose the speeding up due to vectorization in python.
####-	**Choosing mini-batch size**
>	m<= 2000, mini-batch size = m
>		common range - 64 to 1024
		
-	Mini batch should fit in the CPU/GPU memory to avoid reduced/slow performance	
-	**Exponenially Weighted Average**
	-	*V~t~ = (1-B) * V~t-1~ +  theta~t~*
	
-	**Bias Correction in Exponenially Weighted Average**
	-	*V~t~ = V~t~ / (1-B^t^)*
	
-	**Gradient Descent with momentum**	
>		Gradient descent takes a lot of steps to converge to the minima.
>		Therefore, large learnng rate cannot be used in gradient descent to avoid overshooting.
	
	**Without momentum - **
	*W := W - learningrate * dW*
	
	**With momentum - **
	*V~dw~  = B * V~dw~ + (1-B) * dW
	W := W - learningrate * V~dW~
	b := b - learningrate * V~db~
	*
>	This leads to small oscilations in vertical direction and large oscillations in horizontal directions 
>	Hyperparameters - B, learningrate
>	Normally, B = 0.9 works well


-	**RMSprop**
	*S~dw~ = B * S~dw~ + (1-B) * dw^2^ (element wise square)*
	*S~db~ = B * S~db~ + (1-B) * db^2^ (element wise square)*

	w := w - learningrate * dw / [sqrt(S~dw~) + epsilon]
	b := b - learningrate * db / [sqrt(S~db~) + epsilon]
	
	Here, epsilon is a small value to avoid dividing by 0
	
>	db is very large, S~db~ is also very large moreover dw is small and so is S~dw~. 
	 Thus, in above equations, large or small value of dw or db is normalized.
>	This, allows usage of a higher learning rate
	
-	**Adam (Adaptive Moment Estimation) optimization algorithm	**
	-	Combines RMSprop and momentum
		-	**On iteration t:**
					Compute dw, db using current mini batch
					V~dw~  = B~1~ * V~dw~ + (1-B~1~) * dW
					V~db~  = B~1~ * V~db~ + (1-B~1~) * db
					S~dw~ = B * S~dw~ + (1-B) * dw^2^ 
					S~db~ = B * S~db~ + (1-B) * db^2^
					V^corrected^~dw~ = V~dw~/(1-B~1~^t^)
					V^corrected^~db~ = V~db~/(1-B~1~^t^)
					S^corrected^~dw~ = S~dw~/(1-B~2~^t^)
					S^corrected^~db~ = S~db~/(1-B~2~^t^)
					w := w - learningrate * V~dw~/  [sqrt(S~dw~) + epsilon]
					b := b - learningrate * V~db~/  [sqrt(S~db~) + epsilon]
					
		-	**Hyperparameters	**
			learning rate: to be tuned
			B1: 0.9
			B2: 0.999
			epsilon: 10^-8^	
			
-	**Learning rate decay methods**
		Learning rate can be large initially and gradually slow it down as the algorithm approaches convergence
	-	learningrate = (1 / 1 + decayrate * epoch_num) * alpha
	-	learningrate = (0.95)^epoch_num^ * alpha
	-	learningrate = k * alpha / sqrt(epoch_num) 	
	-	Manual decay
	
####-	Problem of local optima
	-	If you are training a neral network with lets say, 20000 parameters then it highly unlikely that the algorithm gets stuck in a local optima.
	-	Out of the 20000 directions atleast 1 will have a significant gradient to guide towards minima.
	-	Such points are called as saddle points
	- 	Training problem occurs at plateaus where the gradient is very low and training slows down.




	