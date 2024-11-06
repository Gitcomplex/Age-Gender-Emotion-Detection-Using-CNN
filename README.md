## Project Overview

This project uses Convolutional Neural Networks (CNNs) to predict age ranges, gender, and emotions from human facial images. The model is trained on popular datasets and deployed using a Flask web application, allowing users to upload images for real-time predictions.

## Features

- **Age Prediction**: Predicts the age range from a facial image.
- **Gender Classification**: Classifies the image as male or female.
- **Emotion Detection**: Recognizes common emotions like happy, sad, and neutral.
- **Web Application**: Provides a user-friendly interface for uploading images and viewing predictions.

## Project Structure

- `.github/workflows/main.yaml`: GitHub Actions workflow for CI/CD, handling code linting, testing, Docker image building, and deployment.
- `templates/`: Contains HTML files (`index.html` for image uploads, `result.html` for displaying predictions).
- `app.py` & `main.py`: Flask application files, loading the models and processing images for predictions.
- `deployment-steps.txt`: Instructions for deploying the application on AWS using EC2 and ECR.
- `Dockerfile`: Defines a Docker image with the application environment.
- `requirements.txt`: Lists the dependencies needed for the project.

## Dataset

The model is trained using three datasets:

- **UTK Face Dataset**: Used for age and gender prediction.
- **Facial-Age Dataset**: Provides labeled age data.
- **CT+ Dataset**: Used for emotion detection.

### Preprocessing

Images are resized and converted to grayscale before inputting into the CNN models:

- **Age Model**: 200x200 pixels
- **Gender Model**: 100x100 pixels
- **Emotion Model**: 48x48 pixels

## Model Architecture

The CNN architecture used for this project includes:

1. Multiple Conv2D layers with increasing filter sizes (32, 64, 128, 256).
2. MaxPooling layers following each Conv2D layer to reduce dimensionality.
3. A fully connected Dense layer.
4. Output layer with softmax activation for classifying emotions, age range, and gender.

## Performance Metrics

- **Age Detection Accuracy**: 82%
- **Gender Classification Accuracy**: 90%
- **Emotion Detection Accuracy**: 97%

## Usage

### Running the Project Locally

1. **Install Requirements**:

   ```bash
   pip install -r requirements.txt
   ```

2. **Run the Flask App**:

   ```bash
   python main.py
   ```

3. **Access the Application**: Open your browser and navigate to http://localhost:5000

## Docker Deployment

1. **Build Docker Image**:

   ```bash
   docker build -t age-gender-emotion-app .
   ```

2. **Run Docker Container**:
   ```bash
   docker run -p 80:80 age-gender-emotion-app
   ```

## Deployment Guide (AWS)

    Follow these steps for AWS deployment:

    Create IAM User: Set up permissions for EC2 and ECR.
    Create ECR Repository: Store the Docker image.
    Launch EC2 Instance: Install Docker on EC2 and configure it as a GitHub runner.
    Push Docker Image to ECR: Build and push the image for deployment.
    Run Docker on EC2: Pull and run the image to serve the application.
    For detailed steps, refer to deployment-steps.txt.

## GitHub Actions CI/CD

    The project uses GitHub Actions to automate testing and deployment:

    Continuous Integration: Lints code and runs unit tests.
    Continuous Delivery: Builds and pushes Docker image to ECR.
    Continuous Deployment: Deploys to EC2 using a self-hosted runner.

## Dependencies

    The project requires the following packages:

    Flask
    TensorFlow
    Keras
    Pillow
    NumPy
    OpenCV
