# Data Processing on Titanic Dataset

## About this project:

To practice data processing is one of the purposes of this project.
The other reason is to see how PCA (Principal Component Analysis) affects machine learning models' performance.
I trained 4 kinds of models on 2 kinds of dataset (with PCA and without PCA).

## The dataset:

Titanic dataset: https://www.kaggle.com/c/titanic/data<br>

- train.csv: Rows: 891, Cols: 11, (memory usage: 83.5+ KB)
- test.csv: Rows: 418, Cols: 10, (memory usage: 35.9+ KB)
- gender_submission.csv: Rows: 418, Cols: 1, (memory usage: 6.5 KB)

## Useful website:

Titanica: https://www.encyclopedia-titanica.org/titanic-deckplans/profile.html<br>
<img width="1440" alt="whole" src="https://user-images.githubusercontent.com/44624585/61586472-a9114180-ab29-11e9-8483-195db549a06e.png"><br><br>

## Variables in the dataset

| Variables | Definition                               | Data type | Key                                            |
| --------- | ---------------------------------------- | --------- | ---------------------------------------------- |
| Survived  | Survived                                 | int       | 0 = No, 1 = Yes                                |
| Pclass    | Ticket class                             | int       | 1 = 1st, 2 = 2nd, 3 = 3rd                      |
| Name      | Name                                     | str       |                                                |
| Sex       | Sex                                      | str       |                                                |
| Age       | Age in years                             | float     |                                                |
| Sibsp     | # of siblings/spouses abroad the Titanic | int       |                                                |
| Parch     | # of parents/children abroad the Titanic | int       |                                                |
| Ticket    | ticket number                            | str       |                                                |
| Fare      | Passenger fare                           | float     |                                                |
| Cabin     | Cabin number                             | str       |                                                |
| Embarked  | Port of Embarkation                      | str       | C = Cherbourg, Q = Queenstown, S = Southampton |

## What problems we have in the dataset

- Missing Values
- Outliers
- Non-numerical Data
- Multiple Value Ranges

## Missing Values

### Columns that have missing values

There are three columns which have missing values.

- Age
- Cabin
- Embarked

**Solution for `Age` column**
<img width="490" alt="Screen Shot 2019-07-22 at 4 46 40 PM" src="https://user-images.githubusercontent.com/44624585/61672409-5d34d880-aca0-11e9-8da0-73e198b9b0ca.png">

`Pclass` has the biggest absolute corretion with `Age`. So the solution is take the mean of Age of each `Pclass` and insert them into blanks respectively.

**Solution for `Cabin` column**<br>
Get rid of this column.

**Because**
<img width="626" alt="Screen Shot 2019-07-22 at 4 49 54 PM" src="https://user-images.githubusercontent.com/44624585/61672501-c0266f80-aca0-11e9-9e2b-19d7f178e8ea.png">

- It doesn't seem there is a correlation between `Survived`, which is the target variable, and `Cabin`.
- The `Cabin` is missing 77.1% of values in the column. So it is hard to fill.

**Solution for `Embarked` column**<br>
The column is missing only two values so I am going to fill the two blanks with `S` which is the place where most people got board from.
<img width="630" alt="Screen Shot 2019-07-22 at 4 53 00 PM" src="https://user-images.githubusercontent.com/44624585/61672630-2e6b3200-aca1-11e9-89c0-b2dd563c3585.png">

## Outliers

The minimum and maximum of `Fare` seem something wrong.
<img width="516" alt="Screen Shot 2019-07-22 at 4 55 33 PM" src="https://user-images.githubusercontent.com/44624585/61672714-8c981500-aca1-11e9-95f2-884166b0e72d.png">

<img width="649" alt="Screen Shot 2019-07-22 at 4 57 01 PM" src="https://user-images.githubusercontent.com/44624585/61672758-be10e080-aca1-11e9-9f78-c85a2c5de624.png">

**Solution for `Fare`**<br>
By using DataFrame and [Titanica](https://www.encyclopedia-titanica.org/titanic-deckplans/profile.html), which is the useful site, try to find the fare of rooms whose size and shape are similar to the size of rooms whose `Fare` is missing.
If can't find them, use mean of fare of each `Pclass` because they are correlated with each other.

## Non-Numerical Data

In the dataset I use for training, there are two columns which have non-numerical values.
<img width="621" alt="Screen Shot 2019-07-22 at 5 03 04 PM" src="https://user-images.githubusercontent.com/44624585/61672994-9f5f1980-aca2-11e9-9205-e2db031dd606.png">

- `Sex`: Usually, sex is not dealt with ordinal variable, but I am going to deal with sex as an ordinal variable here because the female has more priority to be rescued like the privious plot shows. {male: 0, female: 1}
- `Embarked`: This is not ordinal variable so I am going to use one-hot.

## Multiple Value Ranges

To make them in a range between 0 and 1, use Min-Max Normalization.<br><br>

$$
y = \frac{x - x_{min}}{x_{max} - x_{min}}
$$

<br><br>
Where<br>
$y: $is the normalized value of x
$x: $is a value
$x_min: $is the minmum in a column
$x_max: $is the maximum in a column

## Others

I also use PCA in order to summarize the dataset and to reduce the feature dimensions.
And train models, Decision Tree, Random Forest, KNN, and NN on both of dataset without PCA and with PCA, and compared them by actually submitting the results to [Kaggle](https://www.kaggle.com/c/titanic/overview).
