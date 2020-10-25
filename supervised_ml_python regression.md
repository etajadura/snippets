# Regression

## Linear Regression

### Preparing data
```python
# Input
X = df[['TotalSF']] # pandas DataFrame
# Label
y = df["SalePrice"] # pandas Series
```

### Load the library
```python
from sklearn.linear_model import LinearRegression
```

### Create an instance of the model
```python
reg = LinearRegression()
```

### Fit the regressor
```python
reg.fit(X,y)
```

### Do predictions
```python
reg.predict([[2540],[3500],[4000]])
```

## K nearest neighbors
```python
# Load the library
from sklearn.neighbors import KNeighborsRegressor
# Create an instance
regk = KNeighborsRegressor(n_neighbors=2)
# Fit the data
regk.fit(X,y)
```

## Decision Tree
Main parameters
* Max_depth: Number of Splits
* Min_samples_leaf: Minimum number of observations per leaf

```python
# Load the library
from sklearn.tree import DecisionTreeRegressor
# Create an instance
regd = DecisionTreeRegressor(max_depth=3)
# Fit the data
regd.fit(X,y)
```
# Random Forest
```python
# Load the library
from sklearn.ensemble import RandomForestRegressor
# Create an instance
clf = RandomForestRegressor(max_depth=4)
# Fit the data
clf.fit(X,y)
```

# Gradient Boosting Tree
```python
# Load the library
from sklearn.ensemble import GradientBoostingClassifier
# Create an instance
clf = GradientBoostingClassifier(max_depth=4)
# Fit the data
clf.fit(X,y)
```


```

# Metrics
## Regression

### MAE
```python
# Load the scorer
from sklearn.metrics import mean_absolute_error
# Use against predictions
mean_absolute_error(reg.predict(X_test),y_test)
```

### MAPE
```python
np.mean(np.abs(reg.predict(X_test)-y_test)/y_test)
```

### RMSE
```python
# Load the scorer
from sklearn.metrics import mean_squared_error
# Use against predictions (we must calculate the square root of the MSE)
np.sqrt(mean_squared_error(reg.predict(X_test),y_test))
```

### Correlation
```python
# Direct Calculation
np.corrcoef(reg.predict(X_test),y_test)[0][1]
# Custom Scorer
from sklearn.metrics import make_scorer
def corr(pred,y_test):
return np.corrcoef(pred,y_test)[0][1]
# Put the scorer in cross_val_score
cross_val_score(reg,X,y,cv=5,scoring=make_scorer(corr))
```

### Bias
```python
# Direct Calculation
np.mean(reg.predict(X_test)-y_test)
# Custom Scorer
from sklearn.metrics import make_scorer
def bias(pred,y_test):
return np.mean(pred-y_test)
# Put the scorer in cross_val_score
cross_val_score(reg,X,y,cv=5,scoring=make_scorer(bias))
```
