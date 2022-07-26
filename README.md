# Gender-classification-for-jobs

data is read and formatted and saved in [data.pkl](data.pkl) using [preprocess.ipynb](preprocess.ipynb)

to read data.pkl use
```
import pickle
import numpy as np
with open("data.pkl",'rb') as f:
  data = pickle.load(f)
```

similarly if any data needed to be saved use 
```
import pickle
with open("filename.pkl",'wb') as f:
   pickle.dump(data,f)
```