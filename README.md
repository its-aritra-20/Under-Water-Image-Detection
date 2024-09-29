1. Can you explain your underwater image detection project?
In this project, I developed a system for underwater image detection and enhancement using a U-NET architecture based on CNN. The task was to improve the quality of degraded underwater images by transforming them into clearer versions, similar to filtered reference images.

I had two sets of images:

One set contained 900 underwater images, which had distortions due to water refraction, turbidity, and lighting.
The other set contained corresponding filtered (clearer) versions of the same images.
I trained a U-NET model to map these degraded images to their filtered versions. The U-NET architecture is well-suited for this task because of its ability to capture fine details and context in images, thanks to its symmetrical structure—downsampling (encoder) to capture features, and upsampling (decoder) to restore the spatial dimensions.

I split the dataset into 80% training and 20% testing. I also compared the performance of the model using three different loss functions: Mean Squared Error (MSE), Peak Signal-to-Noise Ratio (PSNR), and Structural Similarity Index (SSIM). PSNR gave the best results, as it focuses on the pixel-to-pixel differences between the original and predicted images, which helped in recovering clearer images with less noise.

2. What are the filters used in the CNN and how do they work?
In CNN, filters or kernels are small matrices (for example, 3x3, 5x5) that slide across the input image, performing convolutions. The main purpose of these filters is to detect specific features from the image, such as edges, corners, textures, and more complex patterns as the network goes deeper.

Convolutional Filters: Each convolutional layer applies multiple filters to the input image. Initially, filters may detect basic features like edges (horizontal or vertical), but as we progress through the layers, they capture more complex features like textures, shapes, and object parts. This helps the model to “understand” the spatial structure of the image.

Pooling Layers: After applying filters, the output typically goes through pooling layers (like max-pooling), which reduce the spatial dimensions, making the model more efficient while keeping important information.

In the case of U-NET, convolutional filters in the encoder part capture features at multiple levels, and these features are passed to the decoder part, which restores the image resolution to its original size. The filters help the model understand and recover the lost information in the underwater images.

3. Why did you choose the U-NET model for this task?
I chose U-NET because it is specifically designed for tasks that require pixel-level precision, like image segmentation and restoration. The U-NET architecture consists of two main parts:

Encoder: This part downsamples the input image using convolutional layers, which allows the network to learn abstract and hierarchical features.
Decoder: This part upsamples the feature maps to the original image size and performs pixel-wise classification or restoration.
U-NET's unique feature is the use of skip connections, which link layers from the encoder directly to the decoder, helping retain important spatial information. This is especially useful for restoring fine details in images, which is critical for underwater image enhancement where small features can be easily lost during processing.

4. Why did PSNR give the best result compared to MSE and SSIM?
PSNR (Peak Signal-to-Noise Ratio) gave the best result in my case because it focuses on the ratio between the maximum possible pixel value and the noise level in the image. For my project, PSNR was better suited because the objective was to minimize the overall distortion or noise in the restored images.

MSE: Measures the average squared differences between the predicted and actual pixels. While it's simple, it doesn’t always reflect human perception well, especially when restoring visual images.

SSIM: Focuses on the structural similarity between images. Although SSIM is good for tasks requiring structural preservation, underwater images often suffer from severe noise and color distortions, which PSNR handles better.

In underwater image enhancement, where visual quality and clarity are more critical than structural integrity, PSNR performed better, as it is more sensitive to overall image quality and pixel-wise noise.

5. What challenges did you face during this project?
One of the major challenges was dealing with the limited dataset size. With only 900 images, the model had limited diversity in learning, which could affect its generalization to new underwater images.

Another challenge was tuning the U-NET model, especially deciding the number of layers and filters. If the network was too shallow, it wouldn’t capture complex underwater distortions. If it was too deep, overfitting became a risk due to the small dataset.

Choosing the best loss function was also tricky. Initially, MSE did not give satisfactory results because it only focused on pixel-wise differences. Through experimentation, I found that PSNR worked best for balancing clarity and quality.

Suggested Interview Questions:
Why did you use a U-NET instead of a simpler CNN?

U-NET was chosen due to its ability to restore images with pixel-level precision, thanks to its skip connections. These skip connections help preserve important spatial details that might otherwise be lost during the downsampling process in a traditional CNN.
How did you handle overfitting with a relatively small dataset?

To handle overfitting, I applied techniques like data augmentation (rotation, flipping, color jittering) to artificially increase the diversity of the dataset. I also used regularization techniques like dropout and early stopping to prevent the model from memorizing the training data.
What kind of data augmentation did you use?

I used basic augmentation techniques such as horizontal and vertical flipping, random rotations, and brightness adjustments to simulate different underwater conditions. This helped the model generalize better to unseen data.
Can you explain how skip connections work in U-NET?

Skip connections in U-NET directly link layers from the encoder to the decoder at corresponding levels. This allows the model to combine both high-level abstract features (from deeper layers) and low-level spatial features (from earlier layers), improving the accuracy of pixel-wise predictions.
