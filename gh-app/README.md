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


