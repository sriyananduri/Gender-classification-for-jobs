# Gender-classification-for-jobs

data is read and formatted and converted to gender and saved in [GenderData.pkl](GenderData.pkl)

to read GenderData.pkl use
```
import pickle
import numpy as np
with open("data.pkl",'rb') as f:
  data = pickle.load(f)
```

the loaded data obj is a dict with company names as keys and round number as subkeys in them
as 1,2,3,4... where 1 is the last round and 2 is the last before and so on and inside

data[company][round] we will have an array of 0s and 1s 
0s - female
1s - male