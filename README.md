# s3\_rekog_tagger

This [AWS Lambda](https://aws.amazon.com/lambda/) code will extract up to the top 10 [Amazon Rekognition](https://aws.amazon.com/rekognition/) labels (which is the maximum number of tags supported by S3) and input the [label and confidence] (https://aws.amazon.com/rekognition/faqs/#object-and-scene-detection) rating into the [tag field](http://docs.aws.amazon.com/AmazonS3/latest/dev/object-tagging.html) of a S3 object.

As example, I uploaded the AWS Snowmobile image to a path in S3 where s3\_rekog_tagger is running. The sample image used is below:

![alt text](https://awsdmg.com/images/snowmobile.jpg "Rekognition Sample Image")

The original image file on S3 has no tags, which is shown by issueing the following command:

<pre>~ aws s3api get-object-tagging --bucket mys3bucket --key snowmobile.jpg --version-id 0
{
    "TagSet": []
}
</pre>

After the "s3\_rekog_tagger code runs, the following S3 tags are attached with the object directly:

<pre>~ aws s3api get-object-tagging --bucket mys3bucket --key snowmobile.jpg --version-id 0
{
    "TagSet": [
        {
            "Value": "86.9829177856",
            "Key": "Vehicle"
        },
        {
            "Value": "51.9373130798",
            "Key": "Van"
        },
        {
            "Value": "52.5564842224",
            "Key": "Motor"
        },
        {
            "Value": "96.5879440308",
            "Key": "Transportation"
        },
        {
            "Value": "52.3429946899",
            "Key": "Tow Truck"
        },
        {
            "Value": "86.9829177856",
            "Key": "Truck"
        },
        {
            "Value": "51.9373130798",
            "Key": "Caravan"
        },
        {
            "Value": "52.5564842224",
            "Key": "Engine"
        },
        {
            "Value": "52.5564842224",
            "Key": "Machine"
        },
        {
            "Value": "86.9829177856",
            "Key": "Trailer Truck"
        }
    ]
}
</pre>