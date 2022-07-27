# Gender-classification-for-jobs

the dataset has been taken from placement cell mails and for privacy
reasons all its processing code and data is in a private repo

the dataset consisted of names of students who passed through each round
we data from four companies as such and cleaned it so it only has names
in it and using the name
[LSTMClassifier_IndianNames.ipynb](LSTMClassifier_IndianNames.ipynb)
model we trained and and model weights and training dataset are public
we used the model to classify the names into male and female the model
had an accuracy of 90% on 50 epochs

Then we took the classifed gender and summarized it into number of male
and females in a single round then we reformatted it array has each
company in array and in that 2 subarray one for male other for female
numbers in each rounds that data is stored in
[GenderDataPublic.pkl](GenderDataPublic.pkl)

``` {.python}
import pickle
import matplotlib as mpl
mpl.rcParams['figure.figsize'] = (10,8)
mpl.rcParams['axes.grid'] = False
import matplotlib.pyplot as plt
```

``` {.python}
with open("GenderDataPublic.pkl","rb") as f:
  data = pickle.load(f)
```

``` {.python}
data
```

    [[[23, 11, 2], [47, 26, 7]],
    
     [[75, 32, 2], [114, 38, 4]],
    
    [[16, 7, 3, 1], [17, 13, 11, 1]],
    
    [[134, 3], [232, 9]]]


we calculate the likelyhood to goto next round as -100/slope it is
calculated for each round and stored in array which is later used to
show likelyhood

``` {.python}
def slope(y):
  x = [i for i in range(1,len(y)+1)]
  m = []
  for i in range(1,len(y)):
    dm = (y[i]-y[i-1])/(x[i]-x[i-1])
    m.append(round(100/(abs(dm)+0.0001),2))
  return m
```

``` {.python}
def plot(company):
  global data
  f = data[company][0]
  m = data[company][1]
  labels = [i for i in range(1,len(data[company][0])+1)]
  plt.bar(labels,m,align="edge",width=0.4,label="Boys")
  plt.bar(labels,f,align="edge",width=-0.4,label="Girls")
  plt.plot(labels,m)
  plt.plot(labels,f)
  plt.legend(loc='upper right')
  print("the likelyhood score for each round are as follows : \n", {'Boys':slope(m),'Girls':slope(f)})
```

``` {.python}
plot(0)
```

    the likelyhood score for each round are as follows : 
     {'Boys': [4.76, 5.26], 'Girls': [8.33, 11.11]}

![](images/ff0b8b9b44b2a2704dd261bf70db84ef700e896d.png)


``` {.python}
plot(1)
```

    the likelyhood score for each round are as follows : 
     {'Boys': [1.32, 2.94], 'Girls': [2.33, 3.33]}

![](images/a812d0362dc74eb9308ab62623d9177e45bc7263.png)

``` {.python}
plot(2)
```

    the likelyhood score for each round are as follows : 
     {'Boys': [25.0, 50.0, 10.0], 'Girls': [11.11, 25.0, 50.0]}

![](images/a2e12f1654768a6c29131a4eedbf466d94b55956.png)



``` {.python}
plot(3)
```

    the likelyhood score for each round are as follows : 
     {'Boys': [0.45], 'Girls': [0.76]}
 
![](images/efa1b4986a1476af3875c843bb04a79ed72c777c.png)

# Conclusion : 
Boys are less likely to get through the last rounds than
women which usually are interview and HR rounds but boys are more likely
sometimes in the earlier rounds

