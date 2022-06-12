# BBDC_2022

## Link : https://bbdc.csl.uni-bremen.de/index.php/15-bbdc-2022/39-aufgabenstellung-2022

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
