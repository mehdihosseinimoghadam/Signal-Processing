# Signal-Processing
Signal Processing with Python and Librosa


#1) Voice Reconstruction Using Vq-VAE

This notebook proposes a method on how to reconstruct speech using vq-vae which has been first introduced by [ Oord et. al](https://arxiv.org/abs/1711.00937).



![picture](https://drive.google.com/uc?export=view&id=1XFC5_OYnwge7g14jmKZqHaBwuajsVDyP)



#2) Vq-VAE vs VAE
Main difference between Vq-VAE & VAE is that VAE learns a continuous latent representation of a given dataset, but Vq-VAE learns a discrete latent representation of dataset.  



#3) Architecture


![picture](https://drive.google.com/uc?export=view&id=1hVMCRd4ZeBMM581iLa5ZKV1C-gT4IUsQ)


- At the begining, encoder takes a batch of images with input shape of $X:(n, h, w, c)$ and outputs $Z_{e}:(n, h, w, d)$

- Then vector quantization layer takes $Z_{e}$ and for each vector in $Z_{e}$ it selects the nearest vector from the codebook based on $L_{2}$ norm and outputs $Z_{q}$ 

- Finally decoder takes $Z_{q}$ and reconstructs the input $X$.

#4) Detailed View on Vq-VAE Architecture




![picture](https://drive.google.com/uc?export=view&id=1a---6D9Nzvf7VJpfR_zDGujXSpJwG6cJ)





- Reshaping: First of all we need to reshape input from $(n, h, w, d)$ to $(n*h*w, d)$.

- Calculating Distances: For each of d-dimensional vectors, we calculate their distance from each k, d-dimensional vectors in codebook and get a matrix of $(n*h*w, k)$.

- Argmin: Next for each row of the matrix, we apply argmin function to get the nearest vector index from codebook and do one-hot encoding no each row (in fact the value of the nearest vector will be 1 and rest would be 0).

- Index from Codebook: After that we multiply the one-hotted matrix to the whole codebook and we get a matrix of $(n*h*w, d)$ dimension.

- Finally we reshape $(n*h*w, d)$ to $(n, h, w, d)$ and give it to the decoder to reconstruct the input data 



#5) Some High Resolution Constructed Images


![picture](https://drive.google.com/uc?export=view&id=1rAicXUoCWrLEKtA-Wyvwj2ydNhsbQzk3)


### References
[1] https://shashank7-iitd.medium.com/understanding-vector-quantized-variational-autoencoders-vq-vae-323d710a888a

[2] https://arxiv.org/pdf/1711.00937.pdf
