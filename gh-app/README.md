# WP

## More content

# PR Processing and GCP Upload GitHub Action

## Overview

This GitHub Action automates the process of capturing pull request (PR) information and uploading it to a Google Cloud Platform (GCP) storage bucket. It runs on every pull request to the `main` branch, creating a new file containing PR metadata and the git diff, then uploading this file to a specified GCP bucket.

## Features

- Captures PR number and title
- Records the creation timestamp
- Includes the full git diff of the PR
- Generates a unique filename for each PR, including:
  - PR number
  - Timestamp
  - Short Git SHA
- Uploads a new file to the specified GCP bucket for each PR

## Prerequisites

Before you can use this action, you need to have the following:

1. A Google Cloud Platform (GCP) account
2. A GCP project with Cloud Storage enabled
3. A GCP service account with permissions to upload to Cloud Storage
4. A GCP storage bucket to receive the uploads

## Setup

### 1. Create a GCP Bucket

If you haven't already, create a GCP bucket to store your PR information:

1. Go to the [Google Cloud Console](https://console.cloud.google.com/)
2. Navigate to Cloud Storage > Buckets
3. Click "Create Bucket"
4. Choose a globally unique name for your bucket
5. Configure other settings as needed
6. Click "Create"

### 2. Set up GCP Service Account

1. In the GCP Console, go to IAM & Admin > Service Accounts
2. Click "Create Service Account"
3. Give it a name and description
4. Assign the "Storage Object Creator" role (or a custom role with necessary permissions)
5. Click "Create"
6. Generate a JSON key for this service account
7. Download and save the JSON key file securely

### 3. Configure GitHub Secrets

Store your GCP credentials and bucket name as GitHub Secrets:

1. Go to your GitHub repository
2. Navigate to Settings > Secrets and variables > Actions
3. Click "New repository secret"
4. Create a secret named `GCP_SA_KEY` with the entire content of the JSON key file as the value
5. Create another secret named `GCP_BUCKET_NAME` with your bucket name as the value

### 4. Add the Workflow File

Create a new file in your repository at `.github/workflows/pr_process_upload.yml` and copy the content of the workflow provided in this repository.

## Usage

Once set up, this action will run automatically on every pull request to the `main` branch. For each PR, it will:

1. Capture the PR number and title
2. Record the creation timestamp
3. Generate the git diff
4. Create a new file with this information
5. Upload the file to your specified GCP bucket

The uploaded file will have a name in the format:

```
pr_info_PR<number>_<timestamp>_<short-sha>.txt
```

For example: `pr_info_PR123_20230904_152045_a1b2c3d.txt`

Each PR will create a new file in the bucket, allowing you to keep a history of all PRs.

## Customization

You can customize this action by modifying the `.github/workflows/pr_process_upload.yml` file. Some possible modifications include:

- Changing the trigger conditions (e.g., to run on different branches)
- Adding more information to the PR info file
- Modifying the file naming convention
- Adding additional processing steps

## Troubleshooting

If you encounter issues:

1. Check that your GCP service account key is correctly stored in GitHub Secrets
2. Ensure your service account has the necessary permissions on the GCP bucket
3. Verify that the bucket name is correctly set in GitHub Secrets
4. Check the Action logs in GitHub for any error messages

## Contributing

Contributions to improve this action are welcome. Please feel free to submit issues or pull requests.

## License

[MIT License](LICENSE)

