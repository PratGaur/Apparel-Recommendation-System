# Apparel Recommendation System
Explanation of the problem statement and solution:

A user is shown four pictures in a window from a dataset of apparel images. They provide feedback on whether they liked or disliked the individual photos in the window. After taking the feedback, we need to generate four new pictures from the dataset that they are likelier to like.

The solution was implemented through these steps:-
1. Generating Embeddings: We used 512-dimensional embeddings, which were generated using a pre-trained neural network named VGG-16. Input to the network was resized images(512x512), and output was 512-dimensional embeddings.
2. Creating Clusters: The Kaggle dataset we used for testing had 24 classes, so we assumed that creating 24–50 clusters using k-means clustering would be a good starting point. And manual verification of clusters when choosing k as 40 showed items within the clusters formed were relevant to each other. It is also possible to find the optimal number of clusters using the Elbow Method or Silhouette Score, but we stuck with 40 total clusters.
3. Generating new images after user feedback: We used a probability-based model to show the next set of images to the user. Let’s say at time step t_n; we get four images from clusters, Cn1, Cn2, Cn3, and Cn4 (ni may or may not be equal to nk). Suppose the user gives positive feedback to images from Cn1 and, Cn2, then we update the probability of selection from that cluster to 𝞪*0.75/2; here, we have used two as a dividing factor because only two images were given positive feedback. In general, if k out of 4 images were given positive feedback, then we add the probability of selection from that cluster to 𝞪*0.75/k. Here, 𝞪(0<𝞪<1) is the factor by which we define recency bias. We also used the previous five votes with the factor of 𝞪i, where i indicates the timestep before the current step. Note: Only 0.75 is used to update probabilities based on votes because we wanted an image from a random cluster with a probability of 0.25 so the user can explore what he might not have seen before.

<!-- For explanation of the solution, refer this [medium article](https://medium.com/p/283d94f88542#9776-2eb9c8ae202b) and [video](https://www.youtube.com/watch?v=W4TuVaQqBhk) -->

Instructions to run(using Google colab):

1. Upload the 16k images dataset in your Google drive

2. Run the notebook, give the 4D input vector when prompted consisting of your feedback (1 for positive, -1 for negative)
