# ORB (Oriented FAST and Rotated BRIEF)

## Feature Descriptors
- Feature descriptors are algorithms that extract unique characteristics or patterns from images.
- Feature matching is at the base of many computer vision problems, such as object recognition, image matching, or structure from motion.

## Popular Feature Descriptors
 - SIFT (Scale-Invariant Feature Transform)
 - SURF (Speeded Up Robust Features)
 - FAST (Features from Accelerated Segment Test)
 - BRIEF (Binary Robust Independent Elementary Features)
 - ORB (Oriented FAST and Rotated BRIEF)

 ## ORB (Oriented FAST and Rotated BRIEF)

- ORB is a fusion of FAST keypoint detector and BRIEF descriptor with some added features to improve the performance.
- This algorithm was introduced in the paper ORB: An efficient alternative to SIFT or SURF in 2011.
- ORB is rotation invariant and resistant to noise, making it suitable for images with varying orientations and reliable in real-world scenarios with noisy images.
- It is computationally-efficient replacement to SIFT that has similar matching performance, is less affected by image noise, and is capable of being used for real-time performance
- It is chosen over SIFT and SURF due to its lower computational demands, making it suitable for applications with limited resources or real-time processing requirements.
- ORB uses binary values (0s and 1s) to represent image features, SIFT and SURF descriptors typically consist of floating-point numbers

## Applications

It's especially efficient in real-time applications.\
For example, in applications where both speed and accuracy are crucial, such as:
- **Image matching:** Comparing images to find similarities.
- **Object Recognition:** Identifying objects in images and videos.
- **Image Stitching:** Merging multiple images seamlessly.
- **SLAM (Simultaneous Localization and Mapping):** Localization and mapping in robotics and augmented reality.

## How ORB Works
ORB detects key points using the FAST algorithm and then computes BRIEF descriptors for these points.
### Keypoint Detection:
- ORB uses the FAST algorithm for keypoint detection. FAST identifies keypoints by comparing pixel intensities in a circular pattern around each pixel.
- For a pixel 𝑝 with intensity 𝐼(𝑝), if there exist N contiguous pixels in a circle around 𝑝 that are all brighter or darker than 𝐼(𝑝) by a certain threshold 𝑡, it's marked as a keypoint.
<p align="center">|𝐼(𝑝) - 𝐼(𝑞)| > 𝑡</p>


Here, 𝐼(𝑞) represents the intensity of a neighboring pixel 𝑞. If this condition holds for at least N contiguous pixels, p is marked as a keypoint.

![image](./consecutive.png)

### Feature Description
- After detecting keypoints, ORB computes a descriptor for each keypoint to represent its local image characteristics.
- **BRIEF Algorithm:** ORB uses the BRIEF algorithm for feature description, generating binary strings to represent local image features around keypoints.
- BRIEF compares pairs of pixels within a local patch surrounding each keypoint. Binary values (1 or 0) are assigned based on intensity comparisons between the pixels.
- For each pixel pair (𝑝𝑖, 𝑝𝑗) within the patch, the binary value 𝑏𝑖 is determined by their intensity comparison:
   <p align="center">𝑏𝑖={1,   𝑖𝑓 𝐼(𝑝𝑖​)>𝐼(𝑝𝑗​)  <br>
                        0,    𝑜𝑡ℎ𝑒𝑟𝑤𝑖𝑠𝑒)</p>
- Multiple pixel pairs undergo this process, resulting in a binary string representing the BRIEF descriptor for the keypoint.

### Orientation Assignment
- ORB computes the orientation of keypoints to make the descriptors rotation invariant. This means that even if the object in the image is rotated, ORB descriptors can still match correctly.
- It determines the dominant orientation by analyzing gradients around keypoints.
- A histogram of gradient orientations is created, identifying the peak as the dominant orientation.
- Techniques like Sobel or Scharr operators help compute gradient orientations and magnitudes.
- The keypoint's descriptor is computed based on the determined dominant orientation, ensuring robustness to rotation.

<hr>
In summary, ORB efficiently detects keypoints using the FAST algorithm, generates binary descriptors using the BRIEF algorithm, and computes the orientation of keypoints to make descriptors rotation invariant. These properties make ORB a fast and robust algorithm for tasks such as object recognition, image matching, and visual SLAM (Simultaneous Localization and Mapping) in computer vision applications.

---
***
<br />

## Code

This repository contains a Jupyter Notebook ([code.ipynb](./code.ipynb)) that implements the ORB feature descriptor on two images: a query image and a training image. It matches the keypoints detected in these images.

Additionally, it includes a folder named [Image_Retrieving_from_dataset](./Image_Retrieving_from_dataset), which contains another Jupyter Notebook. This notebook demonstrates the process of loading a dataset and extracting ORB feature vectors from all the images. It then allows the user to input a query image, extract its ORB feature descriptor, and match it with the feature descriptors of images of the dataset. The notebook utilizes the Hamming distance similarity metric to calculate distances, sorts the results, and plots the top images with the lowest distances.

