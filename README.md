Deploying a Machine Learning Model with FastAPI
This repository provides a template for serving a machine learning model as a production-ready REST API using FastAPI. The project includes a simple Streamlit application as a client to demonstrate how to interact with the API. The primary focus is on creating a robust, scalable, and well-documented backend service for machine learning predictions.

Key Technologies
FastAPI: A modern, high-performance web framework for building APIs with Python. It's used here to create a robust backend that serves the ML model, handles requests, and provides automatic, interactive documentation.

Pydantic: Powers the data validation within FastAPI. It ensures that all incoming data conforms to the required schema before being processed, preventing common errors and improving API reliability.

Streamlit: A simple framework for building and sharing data apps. In this project, it acts as a client that consumes the FastAPI service, providing a user-friendly interface for demonstration purposes.

Scikit-learn: The library used to train and export the machine learning model.

Project Structure
The project is organized to separate the concerns of the API, the user interface, and the data science components.

.
├── api/
│   ├── main_api.py         # The FastAPI application
│   └── insurance_model.pkl # The trained machine learning model
├── app/
│   └── streamlit_app.py    # The Streamlit UI client
├── data/
│   └── insurance.csv       # The dataset used for training
├── notebooks/
│   └── model_training.ipynb # Jupyter notebook for model training
└── README.md               # This file

Dataset
This project uses the "Medical Cost Personal Datasets" from Kaggle.

Source: Insurance Forecast by Linear Regression on Kaggle

Download the insurance.csv file and place it in the data/ directory.

Setup and Installation
Clone the repository:

git clone https://github.com/your-username/fastapi-streamlit-insurance-app.git
cd fastapi-streamlit-insurance-app

Install dependencies:
It is recommended to use a virtual environment.

python -m venv venv
source venv/bin/activate  # On Windows use `venv\Scripts\activate`
pip install fastapi "uvicorn[standard]" pandas scikit-learn joblib streamlit requests

Running the Application
This project consists of two services that must be run in separate terminal sessions: the backend API and the frontend interface.

Step 1: Run the FastAPI Backend (Core Service)
Navigate to the project's api/ directory in your terminal.

Start the FastAPI server using Uvicorn:

uvicorn main_api:app --reload

The API is now the core service, running at http://127.0.0.1:8000. You can explore and interact with the API directly through its automated documentation at http://127.0.0.1:8000/docs.

Step 2: Run the Streamlit Frontend (Client)
Open a new terminal window and navigate to the project's app/ directory.

Run the Streamlit client application:

streamlit run streamlit_app.py

The user interface will be available in your browser, typically at http://localhost:8501.

Application Workflow
The workflow is centered around the FastAPI service.

A client (in this case, the Streamlit app) sends a POST request with user data in a JSON format to the /predict endpoint of the FastAPI server.

The FastAPI application receives the request.

Pydantic automatically validates the incoming JSON, ensuring it matches the required data types and structure. If validation fails, FastAPI returns a descriptive JSON error.

If the data is valid, the API endpoint processes it, converting it into the format expected by the machine learning model.

The API loads the trained model (insurance_model.pkl) and generates a prediction.

Finally, the FastAPI service returns the prediction in a JSON response to the client, which then displays the result.
