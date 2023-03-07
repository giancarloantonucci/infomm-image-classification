This repository contains an exercise code that I submitted as part of the CDT in Industrially Focused Mathematical Modelling at the University of Oxford. The `imag_class.m` function uses a hybrid facial-recognition algorithm to achieve image classification with the Yale face database (`YaleB_32x32.mat`), containing 2414 photos of 38 people. Users can choose a test set either randomly or by specific indices, using the following commands:

- `imag_class('NumOfPeople', N)`, which randomly selects `N` people from the 38 available to create the test set.
- `imag_class('People', V)`, which creates the test set using images of people indexed in `V`; e.g., `V = [1 3 6]` selects images of person 1, person 3, and person 6.

The remaining images are used to form the training set.

The classification algorithm is built upon three techniques: PCA, LDA, and k-nearest neighbors.

1. [PCA](https://en.wikipedia.org/wiki/Principal_component_analysis) reduces data dimensionality by finding a new orthogonal basis, called the feature space, from training samples. We project both test and training images onto this space, remove the lowest information dimensions, and weight the basis vectors by importance. The mean face is subtracted from every image in the sets before PCA to improve results.

2. The images in the training set that are of the same person make up a _class_. [LDA](https://en.wikipedia.org/wiki/Linear_discriminant_analysis) increases class separability in feature space by searching for a projection that maximizes between-class scatter and minimizes within-class scatter. We compute scatter matrices for each class and build a projection into the LDA subspace based on these. Then, each image is mapped onto this subspace.

3. In the LDA subspace, we use the [k-nearest neighbors](https://en.wikipedia.org/wiki/K-nearest_neighbors_algorithm) algorithm to determine the person represented in each test image by finding the nearest images in the training set.

Finally, the code outputs the percentage success rate.
