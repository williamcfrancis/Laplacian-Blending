# Laplacian Blending
This project is an implementation of the Laplacian pyramid algorithm for blending images. The algorithm is based on the [paper by Burt and Adelson](http://persci.mit.edu/pub_pdfs/pyramid83.pdf) and aims to produce more realistic outputs compared to traditional image blending methods.
The project includes the following steps:

1. Implementation of the reduce and expand operations as the basic building blocks for the Gaussian and Laplacian pyramids.
2. Implementation of the Gaussian pyramid, where the input is an image and the number of levels of the pyramid.
3. Implementation of the Laplacian pyramid, calculated by subtracting the expanded version of the next level from the same level of the Gaussian pyramid, with the exception of the last level.
4. Implementation of the combine function that creates a combined pyramid from two input pyramids using nodes as weights.
5. Implementation of the collapse function that effectively reverses the steps taken to compute the Laplacian pyramid to produce the final blended output image.


## Usage
1. Clone into this repository using `!git clone https://github.com/williamcfrancis/laplacian-blending.git`
2. Open [`laplacian_blending.ipynb`](https://github.com/williamcfrancis/laplacian-blending/blob/main/laplacian_blending.ipynb) using Google colab, Jupyter Notebook or other supporting ipynb editor. 
3. Download the images and load it into the notebook.
4. Run the cells sequentially

## Why Laplacian Blending?
Laplacian blending is a powerful method for blending images because it takes into account the multiscale structure of images. Traditional blending methods, such as cropping and merging, can produce mediocre results. By using the Laplacian pyramid, the algorithm is able to blend images at multiple scales and produce more realistic outputs.

To illustrate this, consider the following two images we want to blend:
![image](https://user-images.githubusercontent.com/38180831/214786063-23dbcacf-afce-4bb8-b73b-6b039c28474a.png)

If we simply crop the left part from one image and the right part from the other and attempt to merge them, we will get a mediocre result as shown below:
![image](https://user-images.githubusercontent.com/38180831/214786221-800f4364-fc62-471f-9d3f-a94ec292ba0e.png)

However, by using the Laplacian pyramid, the algorithm can produce more realistic outputs, like the one shown below:
![image](https://user-images.githubusercontent.com/38180831/214786390-d7b74e96-7f74-4773-a380-098958fd53cd.png)

## Steps
### Reduce and Expand operations
In the first part of the project, we implemented the code for the basic building blocks used by the Gaussian and Laplacian pyramid, the reduce and expand operations. The `reduce` function is achieved by filtering the image with a Gaussian kernel of size 5x5 and then subsampling the image by a factor of 2. The `expand` function, on the other hand, is achieved by creating an image that is twice the size of the original image and filling every other row and column of the new image with the rows and columns of the original image. The new image is then filtered with the same Gaussian kernel as before.

### Gaussian Pyramid
The next step was to implement the Gaussian pyramid. Given an image and the number of levels of the pyramid, the output is a cell containing all the levels of the pyramid. The `gaussian_pyramid` function was implemented by following the steps described in the script and using the reduce function that we had previously implemented.

### Laplacian Pyramid
We then implemented the Laplacian pyramid in the `laplacian_pyramid` function. It is important to note that every level of the Laplacian pyramid comes from taking the same level of the Gaussian pyramid and subtracting the expanded version of the next level, with the exception of the last level, which is the same as the last level of the Gaussian pyramid. The `laplacian_pyramid` function was implemented by using the `gaussian_pyramid`, expand, and reduce functions that we had already implemented.

### Combine Pyramids
The next function, combine, creates a combined pyramid from two pyramids using the nodes as weights. Specifically, for every level d of the pyramid and every pixel (i, j), the combined pyramid is given by the equation:
LS(d, i, j) = GR(d, i, j) * LA(d, i, j) + (1 - GR(d, i, j))* LB(d; i, j)
where LS is the blended Laplacian pyramid, GR is the mask for blending, LA and LB are the Laplacian pyramids for the two input images respectively. The `combine` function was implemented by following the instructions provided in the script and using the functions implemented in the previous steps.

### Collapse Pyramid
Finally, the Laplacian pyramid of the blended image was collapsed into the image output. To accomplish this, we effectively created the reverse operation that we followed to compute the Laplacian pyramid. Starting from the last level of the Laplacian pyramid, we took the expanded version of it and added it to the image of the previous level. This process was repeated until we reached the first level. The collapse function was implemented by following the instructions provided and with this successfully done, we were able to use the script to run the complete Laplacian Blending algorithm.

## Result

![image](https://user-images.githubusercontent.com/38180831/214787455-ae8e92a4-86c3-46a9-9d29-7dba8214a17b.png)
