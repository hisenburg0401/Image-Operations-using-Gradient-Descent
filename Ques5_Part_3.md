# Brief about the code:

Here, alternating least square method is used to solve the matrix factorization problem. The function `factorize()` is defined to solve the matrix factorization problem using alternating least square method. The function takes the following inputs:

- `A`: The matrix to be factorized
- `k`: The number of latent features
- `device`: The device to be used for computation (like cpu or cuda (for gpu))

The function returns the following outputs:

- `W`: The matrix of user features
- `H`: The matrix of item features

Here, we could have made this function more general by making it available for 3 dimentional tensor as well(because of RGB values). But, for the sake of simplicity, we have only considered 2 dimentional tensor(So here we are considering Red, Green and Blue colour as seperate problems and doing alternating least squares on all of them to get the final 3 dimentional matrix).

# Observations:

Here, as we can see from the image that the reconstructed image by alternating least square method is not so good and it is not giving the exact image. This is happening because of the fact that the alternating least square method just tries to minimize the error between the original and the reconstructed image. But, it does not take into account the fact that the image should be smooth and should not have any abrupt changes in the pixel values. This is the reason why the reconstructed image is not so good. So from the image you can see that the prediction made for missing part of the image is not that much good and it is not able to predict the exact image.

![alt text](image.png)

This plot was for a column of the image where we cut the patch. And below is the predicted plot by the alternating least square method.

Note: Here, we have just considered column only but we can also see the same for the rows as well and both will be same because in the alternating least squares we do linear regression over rows and columns by updating values of W and H alternatively.

![alt text](image-1.png)

Here, we can see that the plot is not smooth and does not predict the trend properly and this is happening because of overfitting and as you can notice the part which was not cut was predicted very good and this is happening because only that part is going under training and we are predicting the values for the missing part but when we give the training part to the least square function with high number of features then it tries to fit the training data very well and hence it overfits the data and hence the prediction is not good. So we tried to decrease the number of features but in that case the the whole image coming out was not good so we kept the number of features to the current value where it was giving the best result.

Also, the time taken by the alternating least square method is very high as compared to the gradient descent method. This is because the alternating least square method is not so efficient and it takes a lot of time to converge to the optimal solution as we seen during the lectures that gradient descent is very fast as compared to the alternating least square method because it solves the direct equation $(X^T * X * \theta = X^T * y)$ which takes very much time.

Here, the number of iterations needed for convergence is very less in alternating least square method because it directly solves the equation and gives the optimal solution. So, in each iteration it gives the most optimum solution for W and H and hence it converges very fast.

Another observation which can be made is that if we increase the size of the missing patch then it gives very bad result and this is happening because it is not able to find the trend of the image properly because the missing part is very large and it is not able to predict the trend properly. So, the result is very bad in that case.
