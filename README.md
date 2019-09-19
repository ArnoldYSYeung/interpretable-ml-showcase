# interpretable_ml_showcase
Showcase of Interpretable ML

##  Problem Statement
Say you're trying to classify between images of African and Indian elephants with a machine learning (ML) agent.  The ML agent can definitely tell you what it predicts a certain image is, but you have no way of verifying that the ML agent is correct.  Even more, you have no idea why it classified the image as such.

##  Explainers
Explainers are methods which provide further details to justify the behaviour of a ML agent.  For example, if I wanted to know why the ML agent predicted a certain image to be of an African elephant, I can use different explainers to get different explanations justifying why the such a prediction is made.

##  Justifying a Classification

Consider:

The ML agent classifies this to be an African elephant, with a confidence of 98%.  (Yes, this actually is an African elephant.)  

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_42_class_0_pred_0.018/proto_42.png" alt="An African Elephant" align="middle" width="400"/>

How is the ML agent so certain?

We can look at one type of explanation (LIME), which says that the regions in red contribute the most to the classification of African elephant.  Similarly, the regions in green contribute the most to the classification of Indian elephant.

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_42_class_0_pred_0.018/lime_42.png" alt="An African Elephant" align="middle" width="400"/>

From the image above, we can tell that the elephant was classified as an African elephant because of the regions in the image which represents the elephant.  This is expected, of course, but we can now be certain it's not looking at something else and making the classification. 

But what about that region in the image made the ML agent classify the image as an African elephant?

Using a heatmap explanation (Deep Taylor), we can tell that the ML agent is paying more attention to the tusks, ears, and shape of the elephant. 

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_42_class_0_pred_0.018/heatmap_42.png" alt="An African Elephant" align="middle" width="400"/>

We now look at another explanation (Prototypes) which shows us the "most similar" images in the training set that were classified as African elephants.

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_42_class_0_pred_0.018/proto_42_58.png" alt="An African Elephant" align="middle" width="400"/><img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_42_class_0_pred_0.018/proto_42_2569.png" alt="An African Elephant" align="middle" width="400"/><img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_42_class_0_pred_0.018/proto_42_2727.png" alt="An African Elephant" align="middle" width="400"/>

Oh okay, this is more helpful.  We see that the ML agent has "seen" some images of African elephants facing the camera directly, with a ledge in front of their feet.  Maybe that's why the ML agent thought it was an African elephant, because African elephants face the camera and have ledges in front of their feet.

Wait, in fact, one of the training images is the same elephant in the same location but only a few seconds ahead (or after).  So the ML agent has seen this elephant before and that's why it's so certain.

If we look back at the first explanation, we realize we were lucky in this classification.  If the elephant was facing another direction, but the image still featured the ears of this elephant, the ML agent might have classified it as an Indian elephant.

##  Identifying Bias in a Classification

Now consider this case:

The ML agent now sees this image labelled as Indian elephants, but strangely, it classifies it as African elephants with 89% confident. 

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_361_class_1_pred_0.11/proto_361.png" alt="An African Elephant" align="middle" width="400"/>

Why is that?

Looking at the LIME explanation, we see that the regions in red are most critical for the classification of African elephant: the face and ears.

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_361_class_1_pred_0.11/lime_361.png" alt="An African Elephant" align="middle" width="400"/>

Looking at the most similar images (Prototypes) classified as an African elephant, we see that these images contain two elephants (yes, look more closely at the 3rd one).  [Perhaps the ML agent identified African elephants as more social.](https://medium.com/elp-rumbles/african-and-asian-elephants-exhibit-distinct-social-behavior-patterns-d124d4c58604) Or even images of African elephants are naturally surrounded by a white border (see 1st and 3rd image).

<img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_361_class_1_pred_0.11/proto_361_2123.png" alt="An African Elephant" align="middle" width="400"/><img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_361_class_1_pred_0.11/proto_361_2727.png" alt="An African Elephant" align="middle" width="400"/><img src="https://github.com/ArnoldYSYeung/interpretable_ml_showcase/blob/master/sample_361_class_1_pred_0.11/proto_361_1677.png" alt="An African Elephant" align="middle" width="400"/>

Both of these explanations may provide more insight into why the ML agent classified these as African elephants instead of the ground-truth labelled Indian elephants.  **(Remember, an ML agent makes classifications on more than one feature of the image.)**  Perhaps the ears and head shape of these elephants resemble African elephants more than Indian elephants, and African elephants tend to be more social (at least in the training images).  

In fact, the ground-truth label might have been wrong!  From my 5 minute experience of distinguishing elephants, these elephants do in fact look more like African elephants.

##  Code

Awesome, where's the code so I can copy this into my own ML algorithm?  Unfortunately, the code for generating these images is part of a larger project which is not yet complete, so I can't release it yet.  However, feel free to Google how to implement these explainers.  There's plenty of resources out there!

##  Conclusion
Different explainers can provide different types of explanations, which can provide different insights into the behaviour of an ML agent.  However, many of these explanations currently still require some level of human interpretation and analysis to identify the root cause of a certain behaviours.
