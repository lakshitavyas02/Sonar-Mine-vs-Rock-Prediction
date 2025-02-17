# Sonar Mine vs Rock Prediction

This project aims to classify objects as either a mine or a rock based on sonar returns using logistic regression. The dataset used for this project is the Sonar dataset, which contains 60 features for each instance representing energy reflected at different angles.

## Table of Contents
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [Dataset](#dataset)
- [Model Training](#model-training)
- [Evaluation](#evaluation)
- [Prediction](#prediction)
- [Contributing](#contributing)
- [License](#license)

## Installation

To run this project, you need Python 3.x and the following libraries:
- pandas
- numpy
- scikit-learn

You can install the required libraries using pip:

```bash
pip install pandas numpy scikit-learn
```

## Usage

1. **Clone the repository:**

   ```bash
   git clone https://github.com/yourusername/sonar-mine-vs-rock.git
   cd sonar-mine-vs-rock
   ```

2. **Place the dataset:**

   Make sure the `sonar data.csv` file is in the project directory.

3. **Run the project:**

   You can execute the script directly to train the model and make predictions.

   ```bash
   python sonar_mine_vs_rock.py
   ```

## Project Structure

```
sonar-mine-vs-rock/
│
├── sonar_mine_vs_rock.py
├── sonar data.csv
└── README.md
```

- `sonar_mine_vs_rock.py`: The main script to train the model and make predictions.
- `sonar data.csv`: The dataset file.
- `README.md`: Project documentation.

## Dataset

The Sonar dataset consists of 208 instances, each with 60 features representing the energy reflected at various angles. The label is either 'R' (rock) or 'M' (mine).

## Model Training

The script uses logistic regression to train the model. The steps are as follows:

1. **Loading the dataset:**
   ```python
   sonar_data = pd.read_csv('sonar data.csv', header=None)
   ```

2. **Separating features and labels:**
   ```python
   X = sonar_data.drop(columns=60, axis=1)
   Y = sonar_data[60]
   ```

3. **Splitting the data:**
   ```python
   from sklearn.model_selection import train_test_split
   X_train, X_test, Y_train, Y_test = train_test_split(X, Y, test_size=0.1, stratify=Y, random_state=1)
   ```

4. **Standardizing the features:**
   ```python
   from sklearn.preprocessing import StandardScaler
   scaler = StandardScaler()
   X_train = scaler.fit_transform(X_train)
   X_test = scaler.transform(X_test)
   ```

5. **Training the model:**
   ```python
   from sklearn.linear_model import LogisticRegression
   model = LogisticRegression(max_iter=1000)
   model.fit(X_train, Y_train)
   ```

## Evaluation

The model is evaluated using accuracy scores on both the training and test data.

```python
from sklearn.metrics import accuracy_score

X_train_prediction = model.predict(X_train)
training_data_accuracy = accuracy_score(X_train_prediction, Y_train)
print('Accuracy on training data: ', training_data_accuracy)

X_test_prediction = model.predict(X_test)
test_data_accuracy = accuracy_score(X_test_prediction, Y_test)
print('Accuracy on test data: ', test_data_accuracy)
```

## Prediction

You can make a prediction for a new input instance as follows:

```python
input_data = (0.0307, 0.0523, 0.0653, 0.0521, 0.0611, 0.0577, 0.0665, 0.0664, 0.1460, 0.2792, 0.3877, 0.4992, 0.4981, 0.4972, 0.5607, 0.7339, 0.8230, 0.9173, 0.9975, 0.9911, 0.8240, 0.6498, 0.5980, 0.4862, 0.3150, 0.1543, 0.0989, 0.0284, 0.1008, 0.2636, 0.2694, 0.2930, 0.2925, 0.3998, 0.3660, 0.3172, 0.4609, 0.4374, 0.1820, 0.3376, 0.6202, 0.4448, 0.1863, 0.1420, 0.0589, 0.0576, 0.0672, 0.0269, 0.0245, 0.0190, 0.0063, 0.0321, 0.0189, 0.0137, 0.0277, 0.0152, 0.0052, 0.0121, 0.0124, 0.0055)
input_data_as_numpy_array = np.asarray(input_data)
input_data_reshaped = input_data_as_numpy_array.reshape(1, -1)

prediction = model.predict(input_data_reshaped)
if prediction[0] == 'R':
    print('The object is a Rock')
else:
    print('The object is a Mine')
```

## Contributing

Contributions are welcome! Please fork this repository and submit pull requests.

## License

This project is licensed under the MIT License.
