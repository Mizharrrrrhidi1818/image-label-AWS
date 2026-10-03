# Implementation labelling image using Amazon rekognition AWS
In this project, we will provide image labels where we employ Amazon Rekognition. It will be able to recognize and label images. Amazon Recognition able to identify what it is and label the image.

Automatically recognize and label images with **Amazon Rekognition**, using **Amazon S3** for image storage and the **AWS CLI** for authentication.

![Pipeline](docs/image_labeler_pipeline.jpg)

## Services Used

| Service | Purpose |
|---|---|
| Amazon S3 | Stores the image to be analysed |
| Amazon Rekognition | Identifies objects and generates image labels |
| AWS CLI | Interacts with AWS from the command line (`aws configure`) |

**Estimated time:** 20-30 minutes  
**Cost:** Free (within the AWS Free Tier)

## Project Structure

```
image-label-AWS/
├── image_label.py      # Main Python script
├── requirements.txt    # Python dependencies
├── docs/
│   ├── Project_image_labeler.pdf       # Full step-by-step report
│   └── image_labeler_pipeline.jpg      # Pipeline diagram
├── .gitignore
├── LICENSE
└── README.md
```

## Setup

### 1. Amazon S3
1. In the AWS console (region **eu-north-1**, Stockholm) create a general purpose bucket named `image-labeler-bucket`.
2. Upload the image you want to analyse (e.g. `image-example.jpg`) to the bucket.

### 2. IAM access key
1. Create an IAM user and generate an **access key** (access key ID + secret access key).
2. Give the user permissions for S3 read and Rekognition (e.g. `AmazonS3ReadOnlyAccess`, `AmazonRekognitionReadOnlyAccess`).
3. **Never commit keys to Git or write them in code.**

### 3. Tools (Windows)
- **AWS CLI** (PowerShell): `irm https://awscli.amazonaws.com/v2/install.ps1 | iex`
- **Git:** download from <https://git-scm.com/download/win>, then check with `git --version`
- **Python 3.x** and **Visual Studio Code**

### 4. Clone the repository
In VS Code press `Ctrl+Shift+P` -> **Git: Clone**, then paste:

```
https://github.com/Mizharrrrrhidi1818/image-label-AWS
```

Or from the terminal:

```bash
git clone https://github.com/Mizharrrrrhidi1818/image-label-AWS
cd image-label-AWS
```

### 5. Configure AWS credentials
Open the terminal (`Ctrl + backtick`) and run:

```bash
aws configure
```

Paste your access key ID, secret access key, set the region to `eu-north-1`, and press Enter for the default output format.

### 6. Install dependencies

```bash
pip install -r requirements.txt
```

## Usage

Edit `photo` and `bucket` in `main()` of `image_label.py` if needed, then run:

```bash
python image_label.py
```

The script will:
1. Send the S3 image to Amazon Rekognition (`DetectLabels`)
2. Print each label with its confidence score
3. Show the image with red bounding boxes and labels
4. Print the total number of labels detected

Example output:

```
Detected labels for image-example.jpg:

  Dog (98.12%)
  Pet (98.12%)
  ...
Labels detected: 8
```

## Security Notes
- `.gitignore` excludes credentials, `.env` files and `.aws/` folders.
- If a secret key is ever exposed, deactivate and delete it in IAM and create a new one.
- Delete the S3 bucket and IAM access key when you finish to avoid unexpected charges.

## Documentation
Full walkthrough with screenshots: [`docs/Project_image_labeler.pdf`](docs/Project_image_labeler.pdf)

## License
Released under the [MIT License](LICENSE).
