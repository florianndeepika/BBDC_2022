# Bremen Big Data Challenge_2022

### Link: https://bbdc.csl.uni-bremen.de/index.php/15-bbdc-2022/39-aufgabenstellung-2022

### Executive Summary:
 This report proposes a complete methodology and solution for the task assigned in Bremen Big Data Challenge 2022 (BBDC). BBDC is an annual data analysis competition conducted by University of Bremen, open for universities students in and around Bremen. The task assigned deals with sequential modelling. The provided data consist of two parallel and synchronous data sequences of human movements captured in video and motion capture files. With a block of missing frames which resulted from the absence of several consecutive frames in the appropriate files. The length, number, and placement of the missing frame components varies. There may be a difference in the amount of missing frame blocks between the two data. The goal is to reconstruct missing data from movement sequences recorded with two separate modalities in detail.
 The dataset was provided by Bremen Big Data Challenge Committee. The video data was recorded from the first-person perspective and had a resolution of 96x160 pixels and a frame rate of 30 frames per second (fps). The head motion capture recordings with 9 features parallel to each frame of video data. The values are given in absolute spatial positions. The centre of the room is indicated by the coordinates (0,0,0). Millimetres are the unit of measurement for features.
 We approached this challenge with RNN Multivariate Time Series Forecasting algorithm using LSTM to identify the sequence of missing frames using TensorFlow. After training our model and predicting the missing observations, the predicted values are captured in motion are saved in a single csv file. Similarly, the predicted pixel values from all 39 videos files are saved in another csv file and converted the identified pixels into a video. After the model being designed, trained and prediction, a variety hyperparameters were applied using TensorFlow differing in the topology adopted.
 The obtained results were uploaded to the BBDC 2022 Submission Portal, and the score was then automatically evaluated with an accuracy of 0.3325 after 2 submissions and displayed on the leader board. Separate score for each file was assigned, namely 51% and 33% in motion and video captured.

### Task
 The Bremen Big Data Challenge 2022 deals with the area of sequence modeling. In detail, it is about correctly reconstructing missing data from motion sequences recorded by two different modalities. There are always two parallel and synchronous data sequences for the movements:

Video data with a resolution of 96x160 pixels and largely at a frame rate of 30 frames per second (fps), which were recorded from a first-person perspective.
Motion capture recordings of the head with 9 features parallel to each frame of the video data. The values are given as absolute positions in space. The position (0,0,0) indicates the center of the room. The unit of features is millimeters.
The video data and the motion capture data are each stored in separate files. Several consecutive frames are missing in the respective files and thus form a block of missing frames. The length, number and positions of the missing frame blocks vary. The missing frame blocks between the video data and the associated motion capture data may also vary.
 
### Data details
There are 30 file triples (in the folder "./data"), each consisting of:
Video recording ("s0xxxxx_video.mp4"): Video file with missing frames (missing frames set to zero).
Motion capture recording ("s0xxxxx_mocap.csv"): Motion capture file with missing frames (missing frames set to zero).
Info file ("s0xxxxx_info.csv"): Info file that indicates for each frame whether motion capture data and video data are present or not.

### Delivery
The files "video.mp4" and "mocap.csv" must be filled with the reconstructed frames.
"video.mp4": This template should be filled with the reconstructed video frames of all 30 video files. This creates a video from only reconstructed frames.
"mocap.csv": This template should be filled with the reconstructed motion capture frames of all 30 motion capture files. This creates a motion capture motion sequence of only reconstructed frames.
In addition, there are two files ("all_idx_{video|mocap}_infos.csv") that define which frames in your specifications correspond to which frames of the original video or motion capture files. The order is important here.
For example, the first entry (s037t01,602) in "all_idx_video_infos.csv" states that the first frame in "video.mp4" corresponds to the reconstructed frame 602 of the file "s037t01_video.mp4". The counting method starts at one. Similarly, this applies to the motion capture data.
 
"all_idx_video_infos.csv": For each reconstructed frame in video.mp4, specifies which video file and its frame corresponds to it.
"all_idx_mocap_infos.csv": For each reconstructed frame in "mocap.csv" indicates which motion capture file and its frame corresponds to it.

### Data Analysis
The implementation of the algorithm was performed by two parts. First, we predicted the missing video captured file. Second, the same methodology was followed to predict the missing frames in the motion captured files. The goal of the project is Sequence-to-sequence prediction which involves predicting an output sequence given an input sequence.
Therefore, we considered the input and output sequences as a time series, and then addressed the problem to as multi-step time series forecasting by RNN network. Additionally, in our case there are multiple parallel time series, and a value must be predicted for each.

### Methodology
<img width="851" alt="image" src="https://user-images.githubusercontent.com/63796480/175786621-64ceea73-a8a7-4f5a-96ae-23512ceda2d7.png">

### Approach
<img width="851" alt="image" src="https://user-images.githubusercontent.com/63796480/175786587-7ef76892-f680-4441-b64c-7c5ac6e575d8.png">

### Designing the model
Keras and Tensorflow was used to build neural networks. For next-frame prediction, our model used a previous frame here n_steps = 2, to predict the next new frame.
The LSTM neural network was built by constructing LSTM cells or at least one LSTM layer. Firstly, a Sequential model was initialized, function was defined with the input and output sequences for a LSTM network. Then a batch normalization layer and a dense (fully connected) output layer was developed. The first layer in a Sequential model created was for model to know what input shape it will expect next. This layer receives information about its input shape. The first hidden layer had 120 memory units and the output layer is a fully connected layer. An LSTM model with one LSTM layer of 120 neurons and relu activation functions was created. The LSTM hidden layer returns a sequence of values rather than a single value for the whole input sequence.

### Training the model
Now the model is built. We trained our model for 50 epochs to make predictions on a new instance along with the x and y data. A new random input sequence will be generated each epoch for the network to be fit on. This ensures that the model does not memorize a single sequence and instead can generalize a solution to solve all possible random input sequences for this problem.

### Prediction
Once trained, the network as evaluated on yet another random sequence. The predictions were then compared to the expected output sequence to provide a concrete example of the skill of the system. The LSTM neural network initializes weights with random values and make prediction. Output layer predicted the missing values in Motion captured and video captured files.

### Results
The predicted values in motion captured was saved in a single csv file. Similarly, predicted pixel values from all the 39 videos captured file was saved in one csv file.
Output of Motion capture:
• 9 variables
• 20888 observations

### Output of Video captures:
The predicted pixel values were converted into images. Finally, images which are frames were converted into video file.

• 96x 159 Variables
• 62953 observations
The duration of the final video was 11:39 sec Two submissions were updated in the BBDC file,
<img width="959" alt="image" src="https://user-images.githubusercontent.com/63796480/175786709-7ee17b58-1895-4553-a978-109f19e30642.png">

### Evaluation
The motion capture and video data reconstructed frames are evaluated separately and provide two partial scores. The structural similarity (SSIM) between the reconstructed and original frames is computed and used as an evaluation metric. The submission's final score is based on the following weighting of both sub-scores: 0.5 * SSIM(Mocap) + 0.5 * SSIM = Final Score (Video).

### Conclusion
In the study, we have presented a method to correctly reconstructing missing data from movement sequences recorded with two separate modalities (video and motion captured data). To identify the sequence of missing frames, we used the RNN Multivariate Time Series Forecasting algorithm with LSTM.

### Limitations and Challenges
The dataset provided had 15264 variables which resulted in high computational power when training the large networks. Additionally, dataset must be trained several times to predict the new test set increased the computation cost. Vanishing Gradient Descent was encountered where the motion captured values seems to fade to 0 as the training increased. This was addressed manually by limiting the predicted values to exceed more than 1. In terms of pixels values in the motion captured fie, the output range was exceedingly more than 256 of the pixel value. This was hard coded to capture the pixel value between 0 and 256.
