---
title: Clustering with the k-Means Algorithm
subtitle: Laboratory 5, DEDP
documentclass: scrartcl
fontsize: 12pt
---


# Objective

Implement and use the k-Means algorithm for 
color-based segmentation of images.

# Theoretical aspects

## The k-Means algorithm

Check the lectures.


# Exercises

## Pixel-based clustering

1. Load the color image 'Peppers.tiff' using `imread()`.
Convert the image to `double` and display it
(don't convert to grayscale, leave the colors).

2. Use Matlab's k-Means algorithm to cluster all
the pixel values (each pixel = a group of three values R, G, B)
into 4 groups.
  - Use the `reshape()` function to resize a $M \times N \times 3$
  tensor `I` into a $(M*N) \times 3$ matrix `P`, as follows:
    ```
    P = reshape(I, [], 3);
    ```
  - Use the `kmeans()` Matlab function to do the clustering.
  Read the documentation for more details.

3. Replace each pixel of the image with the *centroid*
of its class. Display the image. How does it look?

4. Change the number of clusters from 2 to 13
and display them in single window with `subplot()`.

## TODO:
- make background of `flower.bmp` image lighter/darker/different color
- replace background of an image with background from another image

## Vector quantization

1. Repeat process but cluster now a group of pixels:
    - Convert each $2 \times 2$ block of pixels into
    a single vector with 12 values. 
    - Perform clustering on these 12-values data
    - Replace each group of $2 \times 2$ pixels with each centroid
    and plot the result.

	
# Final questions

1. Suppose we do exercises 1 - 3 on a grayscale image.
How will it look?

