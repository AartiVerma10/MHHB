# MHHB
Mobile health human behaviour analysis

Dataset taken from kaggle.

## Data Insight
The MHEALTH dataset contains recordings from ten volunteers wearing sensors on their chest, right wrist, and left ankle.

- What it measures: It records acceleration, rate of turn (gyroscope), and magnetic field orientation, plus 2-lead ECG (heart monitoring) data from the chest sensor.

- The Goal: The volunteers performed 12 specific activities—like standing, walking, jogging, cycling, climbing stairs, and various movements (like waist bends or knee bends).

- The Dataset's Job: It serves as a "benchmark" to test how well a computer can "see" or "feel" human movement through sensors rather than cameras.

## What is the program doing?
the notebook is building a Human Activity Recognition (HAR) system. It follows these steps to turn raw sensor numbers into activity labels:

- Label Encoding: It turns text labels like "Walking" or "Sitting" into numbers (0, 1, 2...) so the computer can process them.

- Data Scaling: It uses RobustScaler to normalize the sensor data. Since sensor readings can vary wildly (e.g., a sudden jump in movement), scaling ensures the model isn't "confused" by extreme values or outliers.

- Training & Classification: It uses models like LogisticRegression and KNeighborsClassifier (KNN) to find patterns in the data. For example, it learns that a specific pattern of acceleration from the wrist and ankle sensors almost always corresponds to "Jogging."

- Performance Tracking: the code automates the testing process to compare different models and tune parameters (like finding the best "K" for KNN) to see which one identifies the activities most accurately.

## Why are we doing this? (The Purpose)
The ultimate goal of this kind of research is Automated Health Monitoring. By teaching a computer to recognize activities, you can build systems that:

- Monitor Fitness: Automatically track how much time someone spends running vs. sitting.

- Elderly Care: Detect if someone has fallen or if they haven't moved for an unusually long period.

- Rehabilitation: Check if a patient is performing their physical therapy exercises correctly.

- Personalized Healthcare: Combine motion data with heart rate (ECG) data to provide real-time alerts about a person's health during daily life.



## ML Models used and theory:

## 1. The Linear Foundations

### Logistic Regression
*   **The Intuition:** Imagine you are trying to predict if a student passes or fails based on study hours.
 A straight line might predict a value of $1.5$ or $-0.2$, which makes no sense for a binary "Pass/Fail" (0 or 1).
*   **The Theory:** Logistic Regression passes the linear output through a Sigmoid Function ($1 / (1 + e^{-z})$). This "squashes" any number into the range between 0 and 1, which we interpret as a probability.
*   **Pro Tip:** It assumes a linear relationship. If the data is not linearly separable, it will perform poorly.

### Lasso (L1 Regularization)
*   **The Intuition:** Sometimes the data has hundreds of features (columns), but only 5 are actually useful. Keeping all of them introduces "noise."
*   **The Theory:** Lasso adds a penalty equal to the absolute value of the coefficients to the loss function. This penalty is mathematically "sharp" at zero, which forces the model to set the least important coefficients to exactly 0.
*   **Pro Tip:** Use this when you want a model that performs feature selection for you.

---

## 2. Distance-Based Learning

### K-Nearest Neighbors (KNN)
*   **The Intuition:** "Tell me who your friends are, and I will tell you who you are."
*   **The Theory:** KNN doesn't "learn" a model. During training, it just remembers the dataset. When a new point arrives, it calculates the distance (usually Euclidean) between that point and all others in the training set. It then looks at the $K$ closest neighbors and takes a majority vote.
*   **Pro Tip:** It is a "memory based" learner. It is very slow on large datasets because it has to calculate distances for every single point.

---

## 3. The Boundary Seekers (SVM)

### Support Vector Classifier (SVC)
*   **The Intuition:** Imagine two groups of dots on a table. How do you draw a line to separate them? You could draw many lines, but the "best" line is the one that stays as far away from both groups as possible.
*   **The Theory:** SVM finds the Maximum Margin Hyperplane. The points closest to the line are called "Support Vectors." If you move any other points, the boundary doesn't change—only the Support Vectors define the boundary.
*   **Pro Tip:** If the data is messy, use the Kernel Trick. It projects data into a higher dimension (like moving from 2D to 3D) so that a flat plane can separate the classes.

---

## 4. The Probabilistic Approach

### Gaussian Naive Bayes (GNB)
*   **The Intuition:** It uses Bayes' Theorem calculating the probability of a class given the observed features. It is "Naive" because it assumes every feature is completely independent of every other feature (e.g., in a "Weather" dataset, it assumes "Humidity" has nothing to do with "Temperature").
*   **The Theory:** It calculates the mean and variance of each feature for every class. When a new point comes in, it calculates the likelihood of that point belonging to each class based on the Gaussian (Normal) distribution.
*   **Pro Tip:** It is incredibly fast and works shockingly well on high dimensional data, even though its "naive" assumption is rarely true in the real world.

---

## 5. Tree-Based Models

### Decision Tree
*   **The Intuition:** A game of "20 Questions." Is the person wearing glasses? Yes. Are they over 6 feet tall? No. By asking these questions, you narrow down the possibilities.
*   **The Theory:** The model recursively splits data based on feature thresholds to maximize "Information Gain" (or minimize "Gini Impurity"). It creates a literal tree structure.
*   **Pro Tip:** Trees are easy to understand but very prone to overfitting (they memorize the data rather than learning the patterns).

### Random Forest
*   **The Intuition:** Don't trust one person's opinion. ask a group of 100 experts and take the majority vote.
*   **The Theory:** This is an Ensemble method. It builds dozens or hundreds of Decision Trees, but with two tricks:
    *   **Bagging:** Each tree sees a different random sample of the data.
    *   **Feature Randomness:** Each split in the tree only considers a random subset of features.
*   **Pro Tip:** Because it averages out the errors of many trees, it is much more stable and accurate than a single Decision Tree. It is arguably the most reliable "out-of-the-box" model in machine learning.

---

## Summary for Success
*   **Start simple:** Use Logistic Regression or Naive Bayes to establish a baseline.
*   **Handle complexity:** If the data is non-linear, use Random Forest or SVC.
*   **Reduce noise:** Use Lasso to clean up your features.
