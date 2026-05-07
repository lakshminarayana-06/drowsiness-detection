Driver Drowsiness Detection System

Project Description
This project is a real-time driver drowsiness detection system built using computer vision and machine learning techniques. It analyzes the driver’s facial features such as eye blinking and eye aspect ratio to identify signs of fatigue. When drowsiness is detected, the system provides alerts through notifications and sound to prevent accidents.

Technology Used
Frontend is developed using React with Vite.
Backend is developed using Node.js.
Machine learning models are implemented in Python using OpenCV and related libraries.
The system integrates frontend, backend, and AI modules for real-time monitoring.

Project Structure
The client folder contains the user interface.
The server folder contains backend logic and APIs.
The ML and CV models folder contains Python files like blink_detector and other detection modules.
The hooks folder inside client contains detection-related logic such as drowsiness and face landmark processing.

How to Run the Project

Step 1 Open a terminal and go to the project folder
Type npm install and press Enter

Step 2 Open a new terminal for backend
Type "npm run dev:server" and press Enter

Step 3 Open another new terminal for frontend
Type "npm run dev:client" and press Enter

Step 4 After running frontend you will get a link like http://localhost:5173
Copy and paste it in browser or click the link
The application will open in the browser

Step 5 Run the Python detection model
Open another terminal
Type python blink_detector.py and press Enter

Features
The system detects eye blinking and monitors drowsiness in real time
It shows alerts when the driver is sleepy
It supports sound alerts using buzzer
It provides a simple user interface for monitoring

Advantages
Helps in reducing road accidents
Provides real-time monitoring
Easy to run and understand
Can be extended with more AI features

Disadvantages
Requires camera access
Performance depends on lighting conditions
Consumes system resources
Accuracy may not be perfect in all situations

Conclusion
This project demonstrates how AI can be used for real-world safety applications. It provides a basic but effective solution for detecting driver drowsiness and can be improved further with advanced models and hardware integration
![image alt](https://github.com/lakshminarayana-06/drowsiness-detection/blob/deb5b67342fedc02048ee218fe48fa9e73aaffef/Screenshot%202026-05-07%20113319.png))



































































































