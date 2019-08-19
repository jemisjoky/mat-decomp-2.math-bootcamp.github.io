---
layout:     post
title:      Principle Component Analysis as Matrix Factorization
date:       2019-08-19
summary:    Seeing the PCA as a model example of the SVD.
categories: machinelearning basics matrices
---

## Introduction

Principal component analysis (PCA) is a simple but powerful method for gaining insight into a dataset of multivariate samples. Given a collection of data samples of several observed features, the PCA outputs a new set of features which are linear combinations of the originals. These PCA features are chosen to remove unnecessary correlations present in the original set of features, and are output with positive weights. Features with higher weight will be more relevant for describing our dataset, and choosing only the features with the highest weights gives an effective and general-purpose method of dimensionality reduction within our dataset.

## What's a Matrix Decomposition?

* Why matrices? Because several observations of multiple features can be described as a data matrix of size $n \times p$, for $n$ the number of samples and $p$ the number of features
* Given a matrix (possibly satisfying some conditions), a matrix decomposition is any _algorithmic_ procedure to represent that matrix as a composition of simpler pieces. Different matrix decompositions have very different flavors, depending on what conditions are imposed on the basic pieces
* In the context of a concrete matrix with real-world significance (such as our data matrix), the individual pieces of a matrix decomposition can help us shed light on the real-world phenomena we're observing

## The Singular Value Decomposition, Mathematically

* The SVD exists for any real (or complex) matrix $M$, and represents $M$ as $M = U S V^T$. Here $U$ and $V$ are orthogonal matrices and $S$ a diagonal matrix of singular values (ordered from largest to smallest). $U$ and $V$ can be thought of as a pair of special bases, while $S$ is a collections of weights assigned to each pair of basis vectors
* The columns of $U$ and $V$ are the left and right singular vectors, which live in the column and row spaces (respectively) of $M$
* SVD can be computed in terms of the eigenvalue decomposition of $M M^T$ or $M^T M$. The eigenvectors of these matrices are the left and right singular vectors (respectively) of $M$, and we get the singular values as the square roots of these symmetric matrices
* Exercise: Assuming the SVD exists for any matrix $M$, prove that the eigenvectors of $M M^T$ and $M^T M$ are the same as the left and right singular vectors of $M$
* Exercise: Unlike the SVD, not all matrices can be diagonalized using the eigendecomposition (the matrix ((0, 1), (0, 0)) is a simple counterexample). Prove that the matrices $M M^T$ and $M^T M$ can always be diagonalized, and that we can safely take the square root of their eigenvalues to obtain positive, real singular values (i.e. the eigenvalues are never negative). [NOTE: Assumes the reader already knows something about eigendecompositions and positive matrices]

## Back to the PCA

* Connect those abstract mathematical properties to concrete statistical properties of the PCA, such as the following:
* For a data matrix $M$, the matrix $M^T M$ is the empirical covariance matrix of the distribution of observed features, whose diagonal entries give the variance of each feature and whose off-diagonal entries give the covariances between different features. Describe how the orthogonality of the right singular vectors of $M$ causes the features output by the PCA to be completely uncorrelated from one another
* [MAYBE NOT USEFUL] What about the left singular vectors? These describe the way we can add/subtract different data samples to produce a composite sample which exhibits the "essence" of the corresponding PCA feature
* Using PCA as a dimensionality reduction technique is optimal, in the sense that truncating our feature space to just the top $k$ PCA features keeps the maximum amount of variance (i.e. maximum useful information) in our transformed dataset
* If this is optimal, why use fancy ML methods? Answer: PCA is fundamentally linear, and is therefore limited in a way that deep learning techniques are not

## Cool Applications and Further Reading

* [Eigenfaces](https://en.wikipedia.org/wiki/Eigenface)
* [Good Stack Exchange thread on SVD and PCA](https://stats.stackexchange.com/questions/134282/relationship-between-svd-and-pca-how-to-use-svd-to-perform-pca)
* [Very good post with more nuance about PCA](http://alexhwilliams.info/itsneuronalblog/2016/03/27/pca/)