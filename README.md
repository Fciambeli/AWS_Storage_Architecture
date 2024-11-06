## AWS Storage Architecture.

![AWS Fanout Sample](https://github.com/Fciambeli/AWS_Storage_Architecture/blob/main/Storage%20Architecture.png)

## Description

Here we will talk about storage efficiency using the following services: Bucket S3, Lambda and DynamoDB. 👇

Practical Scenario: Platform with Image Upload.

Imagine a platform where users upload photos in different formats (profile photos, scanned documents, etc.) to be displayed on the system. We want to ensure these images are at a standardized resolution to save on storage costs (480p) and also save money by removing temporary images that will no longer be used.

Architecture:

1 - Upload to Amazon S3: The user uploads the photo in any format to an S3 bucket (bucket-upload). This bucket acts as an entry point, accepting any image file.

2 - Processing with AWS Lambda: Upon receiving the image, S3 automatically triggers an event that triggers a Lambda function. This function resizes the image to 480p, saves the resized image in a second bucket (bucket-optimized), and stores upload information (metadata) in a DynamoDB table.

3 - Storage Savings: After processing, the Lambda function deletes the image from the upload bucket. This step ensures that only optimized images remain stored, reducing costs by automatically freeing up space on S3.

💥Benefits:

✔Storage Cost Optimization: Amazon S3 charges for occupied storage, so by deleting the original images, we achieve significant savings. In a scenario with thousands of daily uploads, this represents a significant reduction in monthly storage expenses.

✔Scalability: The entire architecture is serverless, that is, it automatically handles increases in the volume of uploads without the need for manual intervention or infrastructure overload.

✔Automated Processing: Lambda processes and stores images in seconds, without the need for a dedicated server, ensuring agility and performance.

✔Organization and Ease of Access to Metadata: DynamoDB stores the metadata of each image (image name, dimensions and upload date), facilitating access to this information and allowing simple integration with other applications.

Imagine that a high-resolution image takes up 5 MB of space. With a system that receives 10,000 images per month, temporary storage can easily exceed 50 GB. By automatically removing the original image after processing, the storage required is drastically reduced, ensuring long-term cost savings.📈

We also save on bucket-upload storage, since all images are in standard 480p and not in larger formats.

This architecture combines operational efficiency with savings in a practical and scalable solution. Using these services, companies can manage image processing in an agile and optimized way, reducing costs and maintenance time.

<div style="display: inline_block"><br>
<img align="center" alt="Fabio-Aw" height="60" width="60" src="https://cdn.jsdelivr.net/gh/devicons/devicon@latest/icons/amazonwebservices/amazonwebservices-plain-wordmark.svg"">
