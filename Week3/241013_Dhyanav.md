Task 1 and Task 2 (Done by Dhyanav)

Task 1

The CIFAR10 dataset is already clean, shuffled and neatly labelled. So, I directly moved to data augmentation. I divided 60,000 images of CIFAR-10 into 6 batches of 10,000 each. They were used for flipping, rotating, cropping, adding noise, cut-out and mixup.

Cut-out: I randomly cut a square of 6 by 6 from the image. Using this technique helps the model learn better since it tries to identify an image without a certain part. It reduces dependence on specific parts of the image. I decided to use 6 by 6 after some experimentation. I feel it was in the middle, not too small to be practically ineffective and not too large to remove all key features entirely.

Mixup: It selects a random image and imposes it on chosen images. The formula used is
	Xnew = alpha*X1 + (1-alpha)*X2
Here, Xnew is the final result, X1 is the base image and X2 is the image that is being imposed. After some experimentation, I used alpha = 0.75.

Then, I combined it into the original dataset, doubling its size. Then, I split data. 95,000 images for training, 10,000 for validation and 15,000 for testing.

Now, I moved to task 2

Task 2

ANN:
I started with 2 hidden layers, but gradually increased the layers so it was computationally viable. Finally, there are 4 layers. I also doubled the number of neurons in each layer and stuck with it since it increased accuracy without overfitting.

I trained for 20 epochs. Since, loss is steadily decreasing, implementing early stopping was not useful. Increasing epochs led to an increase in difference between training accuracy and test accuracy. I finally decided to use 20 epochs since the difference was only 5%.

<img width="847" alt="Screenshot 2025-06-08 at 10 27 42 PM" src="https://github.com/user-attachments/assets/48de6120-9be6-4798-8334-673ba48fa91e" />

<img width="485" alt="Screenshot 2025-06-08 at 10 28 03 PM" src="https://github.com/user-attachments/assets/9bc17a50-37d0-4573-9a29-89c66e62f8aa" />

CNN:
I used a similar process as in ANN. Gradually increasing the number of layers and number of neurons in each layer till I was satisfied with the result. I tried implementing early stopping but it was useless as only the last three layers were showing signs of saturation and early stopping evaluates accuracy of three layers before stopping training.

In both, I used ADAM optimiser, so learning rate was not a part of experimentation as ADAM adjusts learning rate accordingly. I increased batch size from 32 to 128 to speed up training while also maintaining accuracy.

<img width="855" alt="Screenshot 2025-06-08 at 10 32 11 PM" src="https://github.com/user-attachments/assets/36d6251a-963b-418b-83cc-0e0d385172d1" />

<img width="486" alt="Screenshot 2025-06-08 at 10 32 23 PM" src="https://github.com/user-attachments/assets/1962f1f8-c693-4770-8880-8d8a8b7da67f" />

On the CNN model, I implemented one-pixel attack. THis is a type of attack where the attacker randomly selects a pixel and manipulates it. It is known to reduce accuracy of the model by a significant margin. But since I implemented cutout in data augmentation, model accuracy only dropped from 92.71% to 84.3%

<img width="424" alt="Screenshot 2025-06-08 at 10 32 41 PM" src="https://github.com/user-attachments/assets/63cbb280-dbf7-4c19-9c76-a5143b0c07ff" />

Task 3-6(Sumit and Shikhar)
AlexNet, LeNet, VGG16(Sumit)

LeNet: ~60K parameters. A shallow network with 2 convolutional layers.
Epochs-15
Batch Size-128

<img width="329" alt="Screenshot 2025-06-08 at 10 15 33 PM" src="https://github.com/user-attachments/assets/0d826292-f940-4792-97b9-4a845d4f5710" />

<img width="350" alt="Screenshot 2025-06-08 at 10 16 07 PM" src="https://github.com/user-attachments/assets/20c8ec4a-3132-475f-9820-b7d74d4fda9b" />

<img width="627" alt="Screenshot 2025-06-08 at 10 16 29 PM" src="https://github.com/user-attachments/assets/d5635bbd-0929-4138-ab3c-302ef1467578" />

AlexNet: ~60M parameters. A deeper architecture with 5 convolutional layers. It handles larger input variations better.
Epochs: Initially tried 15 but it was taking much longer than LeNet so switched to 5.
Batch Size-128

<img width="337" alt="Screenshot 2025-06-08 at 10 16 52 PM" src="https://github.com/user-attachments/assets/b13caf05-8379-4e89-9c5a-e067995141fe" />

<img width="398" alt="Screenshot 2025-06-08 at 10 17 14 PM" src="https://github.com/user-attachments/assets/a79680d8-340d-41f2-bad3-da63779d3403" />

<img width="625" alt="Screenshot 2025-06-08 at 10 17 35 PM" src="https://github.com/user-attachments/assets/e6b4179a-02f0-4de5-bbcc-8cf5b7c6b78a" />

VGG16: ~138M parameters. A very deep model with 13 convolutional layers. 
Epochs: 5(same problem as AlexNet)
Batch Size: 128

<img width="362" alt="Screenshot 2025-06-08 at 10 18 05 PM" src="https://github.com/user-attachments/assets/bf79b566-6467-48f4-ab23-7f8256eae973" />

<img width="285" alt="Screenshot 2025-06-08 at 10 18 20 PM" src="https://github.com/user-attachments/assets/52dfdb51-938d-4898-8566-65cb47fae721" />

<img width="630" alt="Screenshot 2025-06-08 at 10 18 33 PM" src="https://github.com/user-attachments/assets/6aeb706b-0112-4eed-8d13-a0cee3aaf6a0" />

<img width="737" alt="Screenshot 2025-06-08 at 10 19 01 PM" src="https://github.com/user-attachments/assets/26216fc2-8e43-4990-8913-5e40d54bae1b" />

<img width="653" alt="Screenshot 2025-06-08 at 10 19 27 PM" src="https://github.com/user-attachments/assets/b582a14a-3db3-409f-9137-f774fab8234b" />

Conclusion:
-VGG16 gave the best results in terms of accuracy, F1-score, and AUC.
-LeNet was unsuitable for CIFAR-10 due to its simplicity.
-AlexNet was a good balance between complexity and performance.
