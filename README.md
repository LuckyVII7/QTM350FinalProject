## Amazon Rekognition Service in Real-life Application

## Introduction 

We all had this moment, especially in Georgia, with the intense sunlights and abundant rain during the summer, and blurring vision during the night, it is extremely hard to see some of the text on certain signs along the road. However, failure to recognize them creates significant risk for people to drive on the road and also for people driving near them. For example, driving home at night, it is hard for human beings to recognize traffic signals accurately because of the low lighting value as well as high blurring value, which is the main contributor to the night traffic accidents; when encountering rainy weather, it would be even more dangerous. 

As machine learning technology develops, we now can finally touch the threshold of the era of automatic pilot. However, this technology requires precise and accurate recognition of the vision component of the automobiles. In this case, making sure that machine learning models have the strong ability to recognize the traffic signs under all circumstances will be necessary. In this experiment, our group will artificially simulate images of traffic signs in different real-life conditions and test them against our research hypothesis.

## Amazon Rekognition overview

Amazon Rekognition is based on the same proven, highly scalable, deep learning technology developed by Amazon’s computer vision scientists to analyze billions of images and videos daily. It is accessible to everyone and is not limited to ML expertise. This is a simple, easy-to-use API that can quickly analyze any image or video file that’s stored in Amazon S3. Amazon Rekognition is always learning from new data, and the team continually adding new labels and facial comparison features to the service. People can provide an image or video to the Amazon Rekognition API, and the service can identify objects, people, text, and activities. Common use cases for Amazon Rekognition include searchable image and video libraries, face-based user verification, detection of personal protective equipment (PPE), sentiment and demographic analysis, facial search, unsafe content detection, and text detection. It provides benefits of integrating powerful image and video analysis into users’ apps, deep learning-based image and video analysis, scalable analysis and is a more economically efficient choice for users due to no minimum fees or upfront commitments. In our study, we will focus on the “text detection” use case, which enables people to recognize and extract textual content from images.

## How it works

To detect texts in an image, users can call DetectText API and pass an input image. The input image can be provided as an image byte array (base64-encoded image bytes) or as an Amazon S3 object. Rekognition DetectText can detect words in English, Arabic, Russian, German, French, Italian, Portuguese and Spanish, and detect up to 100 words in an image. The DetectText operation request returns the information for the detected text, the relationships between words and lines, the location of text on the image, the confidence score, and the type of the detected text.

The following image shows an example input image and its corresponding output information of the Amazon Rekognition DetectText service.

![image](https://edwardchenproject350.s3.amazonaws.com/SampleImage.jpg)

The blue boxes represent information about the returned response of the detected text and the corresponding location. In this example, Amazon Rekognition detects "IT'S", "MONDAY", "but", "keep", and "Smiling" as words, and "IT'S", "MONDAY", "but keep", and "Smiling" as lines.
Following is the request syntax for Rekognition DetectText API. Users can replace the values of `bucket_name` and `image_name` with the names of their S3bucket and image.

```
import boto3
```
```
client = boto3.client('rekognition')
response = client.detect_text(
            Image={
                'S3Object': {
                    'Bucket': bucket_name,
                    'Name': image_name
                }
            }
        )
```

The response of the DetectProtectiveEquipment API is a JSON structure that includes the following information:
The detected text (DetectedText)
The relationships between words and lines (Id and ParentId)
The location of text on the image (Geometry)
The confidence Amazon Rekognition has in the accuracy of the detected text and bounding box (Confidence)
The type of the detected text (Type)
Users can filter the relevant fields they are interested in using the above keywords for field names. The full response from the DetectText API for this sample image is as follows:

```
{
    "TextDetections": [
        {
            "Confidence": 90.54900360107422,
            "DetectedText": "IT'S",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.10317354649305344,
                    "Left": 0.6677391529083252,
                    "Top": 0.17569075524806976,
                    "Width": 0.15113449096679688
                },
                "Polygon": [
                    {
                        "X": 0.6677391529083252,
                        "Y": 0.17569075524806976
                    },
                    {
                        "X": 0.8188736438751221,
                        "Y": 0.17574213445186615
                    },
                    {
                        "X": 0.8188582062721252,
                        "Y": 0.278915673494339
                    },
                    {
                        "X": 0.6677237153053284,
                        "Y": 0.2788642942905426
                    }
                ]
            },
            "Id": 0,
            "Type": "LINE"
        },
        {
            "Confidence": 59.411651611328125,
            "DetectedText": "I",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.05955825746059418,
                    "Left": 0.2763049304485321,
                    "Top": 0.394121915102005,
                    "Width": 0.026684552431106567
                },
                "Polygon": [
                    {
                        "X": 0.2763049304485321,
                        "Y": 0.394121915102005
                    },
                    {
                        "X": 0.30298948287963867,
                        "Y": 0.3932435214519501
                    },
                    {
                        "X": 0.30385109782218933,
                        "Y": 0.45280176401138306
                    },
                    {
                        "X": 0.27716654539108276,
                        "Y": 0.453680157661438
                    }
                ]
            },
            "Id": 1,
            "Type": "LINE"
        },
        {
            "Confidence": 92.76634979248047,
            "DetectedText": "MONDAY",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.11997425556182861,
                    "Left": 0.5545867085456848,
                    "Top": 0.34920141100883484,
                    "Width": 0.39841532707214355
                },
                "Polygon": [
                    {
                        "X": 0.5545867085456848,
                        "Y": 0.34920141100883484
                    },
                    {
                        "X": 0.9530020356178284,
                        "Y": 0.3471102714538574
                    },
                    {
                        "X": 0.9532787799835205,
                        "Y": 0.46708452701568604
                    },
                    {
                        "X": 0.554863452911377,
                        "Y": 0.46917566657066345
                    }
                ]
            },
            "Id": 2,
            "Type": "LINE"
        },
        {
            "Confidence": 96.7636489868164,
            "DetectedText": "but keep",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.0756164938211441,
                    "Left": 0.634815514087677,
                    "Top": 0.5181083083152771,
                    "Width": 0.20877975225448608
                },
                "Polygon": [
                    {
                        "X": 0.634815514087677,
                        "Y": 0.5181083083152771
                    },
                    {
                        "X": 0.8435952663421631,
                        "Y": 0.52589350938797
                    },
                    {
                        "X": 0.8423560857772827,
                        "Y": 0.6015099883079529
                    },
                    {
                        "X": 0.6335763335227966,
                        "Y": 0.59372478723526
                    }
                ]
            },
            "Id": 3,
            "Type": "LINE"
        },
        {
            "Confidence": 99.47185516357422,
            "DetectedText": "Smiling",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.2814019024372101,
                    "Left": 0.48475268483161926,
                    "Top": 0.6823741793632507,
                    "Width": 0.47539761662483215
                },
                "Polygon": [
                    {
                        "X": 0.48475268483161926,
                        "Y": 0.6823741793632507
                    },
                    {
                        "X": 0.9601503014564514,
                        "Y": 0.587857186794281
                    },
                    {
                        "X": 0.9847385287284851,
                        "Y": 0.8692590594291687
                    },
                    {
                        "X": 0.5093409419059753,
                        "Y": 0.9637760519981384
                    }
                ]
            },
            "Id": 4,
            "Type": "LINE"
        },
        {
            "Confidence": 90.54900360107422,
            "DetectedText": "IT'S",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.10387301445007324,
                    "Left": 0.6685508489608765,
                    "Top": 0.17597118020057678,
                    "Width": 0.14985692501068115
                },
                "Polygon": [
                    {
                        "X": 0.6677391529083252,
                        "Y": 0.17569075524806976
                    },
                    {
                        "X": 0.8188736438751221,
                        "Y": 0.17574213445186615
                    },
                    {
                        "X": 0.8188582062721252,
                        "Y": 0.278915673494339
                    },
                    {
                        "X": 0.6677237153053284,
                        "Y": 0.2788642942905426
                    }
                ]
            },
            "Id": 5,
            "ParentId": 0,
            "Type": "WORD"
        },
        {
            "Confidence": 92.76634979248047,
            "DetectedText": "MONDAY",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.11929994821548462,
                    "Left": 0.5540683269500732,
                    "Top": 0.34858056902885437,
                    "Width": 0.3998897075653076
                },
                "Polygon": [
                    {
                        "X": 0.5545867085456848,
                        "Y": 0.34920141100883484
                    },
                    {
                        "X": 0.9530020356178284,
                        "Y": 0.3471102714538574
                    },
                    {
                        "X": 0.9532787799835205,
                        "Y": 0.46708452701568604
                    },
                    {
                        "X": 0.554863452911377,
                        "Y": 0.46917566657066345
                    }
                ]
            },
            "Id": 7,
            "ParentId": 2,
            "Type": "WORD"
        },
        {
            "Confidence": 59.411651611328125,
            "DetectedText": "I",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.05981886386871338,
                    "Left": 0.2779299318790436,
                    "Top": 0.3935416042804718,
                    "Width": 0.02624112367630005
                },
                "Polygon": [
                    {
                        "X": 0.2763049304485321,
                        "Y": 0.394121915102005
                    },
                    {
                        "X": 0.30298948287963867,
                        "Y": 0.3932435214519501
                    },
                    {
                        "X": 0.30385109782218933,
                        "Y": 0.45280176401138306
                    },
                    {
                        "X": 0.27716654539108276,
                        "Y": 0.453680157661438
                    }
                ]
            },
            "Id": 6,
            "ParentId": 1,
            "Type": "WORD"
        },
        {
            "Confidence": 95.33189392089844,
            "DetectedText": "but",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.06849122047424316,
                    "Left": 0.6350157260894775,
                    "Top": 0.5214487314224243,
                    "Width": 0.08413040637969971
                },
                "Polygon": [
                    {
                        "X": 0.6347596645355225,
                        "Y": 0.5215170383453369
                    },
                    {
                        "X": 0.719483494758606,
                        "Y": 0.5212655067443848
                    },
                    {
                        "X": 0.7195737957954407,
                        "Y": 0.5904868841171265
                    },
                    {
                        "X": 0.6348499655723572,
                        "Y": 0.5907384157180786
                    }
                ]
            },
            "Id": 8,
            "ParentId": 3,
            "Type": "WORD"
        },
        {
            "Confidence": 98.1954116821289,
            "DetectedText": "keep",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.07207882404327393,
                    "Left": 0.7295929789543152,
                    "Top": 0.5265749096870422,
                    "Width": 0.11196041107177734
                },
                "Polygon": [
                    {
                        "X": 0.7290706038475037,
                        "Y": 0.5251666903495789
                    },
                    {
                        "X": 0.842876672744751,
                        "Y": 0.5268880724906921
                    },
                    {
                        "X": 0.8423973917961121,
                        "Y": 0.5989891886711121
                    },
                    {
                        "X": 0.7285913228988647,
                        "Y": 0.5972678065299988
                    }
                ]
            },
            "Id": 9,
            "ParentId": 3,
            "Type": "WORD"
        },
        {
            "Confidence": 99.47185516357422,
            "DetectedText": "Smiling",
            "Geometry": {
                "BoundingBox": {
                    "Height": 0.3739858865737915,
                    "Left": 0.48920923471450806,
                    "Top": 0.5900818109512329,
                    "Width": 0.5097314119338989
                },
                "Polygon": [
                    {
                        "X": 0.48475268483161926,
                        "Y": 0.6823741793632507
                    },
                    {
                        "X": 0.9601503014564514,
                        "Y": 0.587857186794281
                    },
                    {
                        "X": 0.9847385287284851,
                        "Y": 0.8692590594291687
                    },
                    {
                        "X": 0.5093409419059753,
                        "Y": 0.9637760519981384
                    }
                ]
            },
            "Id": 10,
            "ParentId": 4,
            "Type": "WORD"
        }
    ]
}
```

## Hypothesis

1. As we decrease and increase the brightness value of the image, AWS Rekognition will be less able to figure out the content on the sign correctly.

2. As we increase the particle value of the image, AWS Rekognition will be less able to figure out the content on the sign correctly.

3. As we increase the blurring value of the image, AWS Rekognition will be less able to figure out the content on the sign correctly.

## Original Image

The following is our original image for the experiment, it includes one line of address created randomly, and one line of distance also created ramdomly.

![image](https://edwardchenproject350.s3.amazonaws.com/Material.png)

In this experiment we will be adjusting the lighting, particle, and blurring value of it to test the text capturing ability under different circumstances of the Amazon Rekognition Service.

## Architecture diagram

Depending on your experiment setup, you can use different approaches to analyze your on-premises camera feeds for text recognition. Because AWS Rekognition only accepts images as input, you can import image files taken by cameras and analyze them using the AWS Rekognition. You can also set different parameters of the images for experiment. For example, you can change the lighting, dispersion, and so on. This allows you to control the image attribution.
The following architecture shows how you can design a workflow to process images from camera feeds for test recognition.

![image](https://edwardchenproject350.s3.amazonaws.com/QTM350.jpg)

As shown in the diagram, the flow is as followed:
1. Create image files for text recognition with camera;
2. Upload it to a desktop and use photoshop change different parameters of the original image;
3. Save the processed images to your S3 bucket for further analysis;
4. Use AWS Sagemaker Notebook to call for AWS Rekognition service for text analysis in the image;
5. Save the result of the AWS Rekognition service and naked eye to a data frame;
6. Use Python package for regression and data visualization;
7. Convert the results into a blog and upload it as a web page;
8. Create a Github repository for later recreation of the experiment.

## Dataframe Construction 

Our data frame is constructed as follows:

- The image name (Name)
- The types of image processing and modification (type)
    * Change lighting value (L)
    * Change particle value (P)
    * Blurring (B)
- The modification level (level)
- The detected text for the first line (text1)
- The detected text for the second line (text2)
- The confidence score for the first line (confidence1)
- The confidence score for the second line (confidence2)
- The weighted confidence score (confidence)

It should be noticed that the confidence score (confidence) is weighted by the length of each text since there are major differences in the distribution of text line lengths. We will use the weighted confidence score as our target variable to conduct the regression analysis as follows. 

## Regression Analysis

In order to understand how the lighting value, particle value, and blurry value affect the weighted confidence, we conducted linear regression analysis. Our analysis is divided into three parts: particle value,  blurry value, and lighting value.  And based on our visualization and linear regression table, we can draw conclusions on the performances of Rekognition in different scenarios. 

### Particle Value:

![image](https://edwardchenproject350.s3.amazonaws.com/particle+value+fig.png)

From the above diagram, we see that within the range of [0, 300] particle value, the line of best fit is almost horizontal, representing a nearly 0  linear regression coefficient. Thus the line of best fit suggests that with the increase of  particle value, the weighted confidence does not change. And even with the largest particle value 300, the weighted confidence is greater than 99.00, which means that Rekognition can successfully detect all of them. 

![image](https://edwardchenproject350.s3.amazonaws.com/particle+value+table.png)

From the table above, we see that the linear coefficient is 0.000065 and the intercept is 99.3673. Since the  linear coefficient is very close to 0, it indicates that the changes in particle value does not affect the detecting performance and confidence level result of Rekognition. Also we notice that the R-square is 0.024, which is very close to 0. Since R-square value tells how much variation is explained by the model, our small R-square value means that our model only explains 2.4% of variation within the data. However, even though our model does not explain most of our data, we observe that within the range of [0, 300] particle value, the weighted confidence levels are all greater than 99. Thus we can still conclude that the particle value does not affect the performance of Rekognition. 

### blurring: 
Then, we try to explore the relationship between blurring value and confidence. 

![image](https://edwardchenproject350.s3.amazonaws.com/blurring+value+fig+1.png)
![image](https://edwardchenproject350.s3.amazonaws.com/blurring+value+table+1.png)

In general, the line of the best fit is negative with the linear coefficient of -1.0204, which infers that as the blurring value increases, the weighted confidence decreases. Also, R-squared of 0.694 means that   our model explains 69.4% of variation within the data, which infers that the variation is well-explained by the model.

However, if we further observe the graph, before the blurring value of  40, the weighted confidence almost remains unchanged. Thus, to depict the relationship more correctly, we decide to run another linear regression that focuses on the blurring values that are larger than 40. 

![image](https://edwardchenproject350.s3.amazonaws.com/blurring+fig2.png)
![image](https://edwardchenproject350.s3.amazonaws.com/blurring+table+2.png)

After running the linear regression, the linear coefficient changes from -1.0204 to -1.9929, which indicates that the negative relationship becomes more obvious. Also, the R-squared increases from  0.694 to 0.795. With the blurring value of 80, the weighted confidence is only 65.64. What’s worse, after 80, the confidence abruptly drops to 0, which means that after 80, the Rekognition fails to detect the text. Compared to the result in the particle value section, the Rekognition is more sensitive to the change of the blurring values. However, it intuitively makes sense as the blurring value  is more influential to the resolution of the images compared to the particle value. 

### Lighting Value:

We also want to find out the effects of lighting values on the performance of Rekognition.

![image](https://edwardchenproject350.s3.amazonaws.com/lighting+fig1.png)

From the above diagram, we see that within the range of [-300, 300] lighting value, the line of best fit has a negative slope, representing a negative correlation between lighting value and the weighted confidence.  Thus the line of best fit suggests that with the increase of lighting value, the weighted confidence decreases.  Also we notice a sudden drop of weighted confidence in lighting value range [270, 300]. 

![image](https://edwardchenproject350.s3.amazonaws.com/lighting+table+1.png)

From the table above, we see that the linear coefficient is -0.0407 and the intercept is 94.8737. Since the  linear coefficient is very close to 0, it indicates that the changes in lighting value does not strongly affect the detecting performance and confidence level result of Rekognition. Also we notice that the R-square is 0.143, which represents 14.3% of the variation within the data. 

Notice that there is a  sudden change of weighted confidence level with the positive lighting valuel. Also, based on the fact that  only when the absolute value of the lighting value is closer to zero that the picture is closer to the original picture, we decide to run the linear regression model separately with positive lighting value and negative lighting value. 

![image](https://edwardchenproject350.s3.amazonaws.com/positive+lighting+fig.png)

From the diagram above, we see that when the lighting value is  positive,  the line of best fit has a negative slope,  representing  a negative correlation between lighting value and the weighted confidence.

![image](https://edwardchenproject350.s3.amazonaws.com/positive+lighting+table.png)

From the table above, we see that the linear coefficient is -0.1651 and the intercept is 116.8411. Since the  linear coefficient is negative, it indicates that the increase in lighting value decreases the detecting performance and confidence level result of Rekognition. Also we notice that the R-square is 0.275, which represents 27.5% of the variation within the data. Noticing the sudden change of weighted confidence level with the positive lighting valuel, we believe that under extreme bright senario, the Rekognition does not have a good detection of the text. Particularly for the lighting value of 300, the Rekognition fails to detect the text.

![image](https://edwardchenproject350.s3.amazonaws.com/negative+lighting+fig+.png)

From the diagram above, we see that when the lighting value is negative,  the line of best fit has a negative slope,  representing  a negative correlation between lighting value and the weighted confidence. Although this may seem counterintuitive, we see that all weighted confidence levels are greater than 99, which indicates successful detection. Also as we have a very small interval of y axis, the variation of the dataset is exaggerated. 

![image](https://edwardchenproject350.s3.amazonaws.com/negative+lighting+table.png)

From the table above, we see that the linear coefficient is -0.0003 and the intercept is 99.3276. Since the  linear coefficient is very close to 0, it indicates that the changes in negative lighting value does not affect the detecting performance and confidence level result of Rekognition. Also we notice that the R-square is 0.229, which indicates that our model explains 22.9% of variation within the data. Although our model does not explain most of our data, we observe that within the range of [-300, 0] lighting value, the weighted confidence levels are all greater than 99. Thus we can still conclude that the negative lighting value does not affect the performance of Rekognition. 

### Link to the Codebook

https://edwardchenproject350.s3.amazonaws.com/QTM350ProjectCode.ipynb

## Discussion and Conclusion

![image](https://edwardchenproject350.s3.amazonaws.com/conclusion.png)

Based on our analysis and test, Rekognition did a good job detecting the text. According to the linear coefficient table above, the detection function is the most sensitive to the change in blurring value and the least sensitive to the changes in  particle value, which is consistent with human eyes. However, one finding is beyond our expectation. We expect that the results for positive lighting values and negative lighting values should be similar. However, Rekognition performs better when we adjust the negative lighting value compared to the results when we change the positive lighting value. For instance, when the lighting value is 275, the confidence is only 92.84 whereas when the lighting value is -275, the confidence still has 99.43. Our speculation is that the color of our text is white, which forms a strong contrast visually to the black color. Therefore, the text is easier to be detected under a darker background. While we increase the lighting value, the whole picture becomes brighter, and the white text can be very hard to detect. Thus, for future analysis, we can explore how the color of the text may affect Rekognition’s performance. 

Our experiment and test results can provide some insights on the accuration and precision of the recognition used on the automatic pilot. With Rekognition performances of detecting the traffic sign under different particle values, blurry values, and light values, we believe that using Rekognition in autopilot can be very promising. 

For instance, our results indicate successful detection at negative lighting values especially with signals that have white text. Together with a successful detection for text with high particle values, we can conclude that Rekognition can successfully recognize traft signs at night and rainy days. However, relatively poor performance for text with high blurring values and high positive lighting values infer that  under the extreme bright environment or speeding motions, Rekognition may not precisely recognize the text on the traffic sign, leading to possible danger for drivers. As machine learning technology develops, we believe that further investigation and improvement on Rekognition’s performance will lead to a promising future for automatic pilot’s precise and accurate recognition of traffic signs.

## GitHub Repository

https://github.com/LuckyVII7/QTM350FinalProject.git

## Work Cited: 

https://aws.amazon.com/blogs/machine-learning/automatically-detecting-personal-protective-equipment-on-persons-in-images-using-amazon-rekognition/

https://github.com/aws-samples/amazon-rekognition-custom-ppe-detection-with-custom-labels

## Authors Introduction
We are 5 senior students at Emory University taking QTM350 - Data Science Computing class. Our team members are:  Audrey Gong, Cecilia Ting, Duping Gao, Edward Chen, and Lizzy Fang. 

### Xindi Gong
Hi, my name is Xindi Gong, and I also go by Audrey. I am a senior stuent majoring in AMS. You can find me on [Instagram](https://www.instagram.com/xindigong/) or [Linkedin](https://www.linkedin.com/in/xindi-gong-80273b1b9/).
<center>
<img src="https://drive.google.com/uc?id=1vz4SknCzzIwyq4xT523_y2nrE1B0XnV0" alt="https://drive.google.com/uc?id=1vz4SknCzzIwyq4xT523_y2nrE1B0XnV0" width="250" />

### Yujan Ting
Hi, I'm Yujan Ting, and I also go by Cecilia. I'm a senior majoring in AMS and Computer Science. I come from Kunming, a beautiful city in the southwest China , and I also come from Taiwan. I'm a dog person who has three dogs. You can find me on [Instagram](https://www.instagram.com/yujant_/) here!
<center>
<img src="https://drive.google.com/uc?export=view&id=1aZ48EBdMXXV--VqCHMPraqRwuQRHaPCs" alt="https://drive.google.com/uc?export=view&id=1aZ48EBdMXXV--VqCHMPraqRwuQRHaPCs" width="200" />
 
### Duping Gao
Hello, I'm Duping Gao. Currently I am in Beijing, China, which is also my hometown. I'm now a Senior majored Appiled Math & Stats and Economics. I hope I can learn more about cloud computing and related data science knowledge from this course. Here is my [Instagram account](https://www.instagram.com/duping_gao/), and I always share my recent life there. Follow me if you want!
<center>
<img src="https://drive.google.com/uc?id=1UgMIodi4nCgfkTS-hkQK-XDEozA_vdGb" alt="https://drive.google.com/uc?id=1UgMIodi4nCgfkTS-hkQK-XDEozA_vdGb" width="250" />
 
### Lizzy Fang
Hey, I am Lizzy Fang, a senior student majoring in QSS Econ track. I am originally from Beijing China, and in my free time, I love indoor climbing, reading, HBO and gaming. You can find my [Instagram](https://www.instagram.com/lizbittersweet/) here!
<center>
<img src="https://drive.google.com/uc?id=1wB3LUJUcH-UVTveXxP6t8c_rDwnTKOuj" alt="https://drive.google.com/uc?id=1wB3LUJUcH-UVTveXxP6t8c_rDwnTKOuj" width="250" />

### Edward Chen    
Hi, my name is Edward Chen. I am currently a senior student in Emory University My major is AMS, and I also minor in Economics. My favourite game is League of Legends.
<center>
<img src="https://edwardchenproject350.s3.amazonaws.com/EdwardChen.jpg" alt="https://edwardchenproject350.s3.amazonaws.com/EdwardChen.jpg" width="150" />
