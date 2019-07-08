## How to make your embarrassingly parallel processing faster with Python

Maybe there are better ways to do it but I make my preprocessing faster using Python's `multiprocessing` package which works with `pandas` and which made my embarrassingly parallel program four times faster. This package allows you to use all cores on your machine and you will get performance gain depending upon the number of cores on your machine. Below, I am pasting a code snippet that demonstrates how to use this package with `pandas`. As mentioned before, I got performance gain of 4x on my preprocessing task, as I have 4 cores on my laptop.


```
import numpy as np
import multiprocessing as mp
from multiprocessing import cpu_count
import re, time

def normalize(text):
    # Your code for preprocessing 

def run_normalize(df):
    df['text_preprocessed'] = df['text'].apply(normalize)
    return df

def parallelize(df, func):
    data_split = np.array_split(df, cores)
    pool = mp.Pool(cores)
    df_processed = pd.concat(pool.map(func, data_split))
    pool.close()
    pool.join()
    return df_processed

start = timer()
print('Start time: ', start)
cores = cpu_count()
df = pd.read_csv(<YOUR INPUT CSV>)

# Preprocess the rows in parallel 
df_processed = parallelize(df, run_normalize)
end = timer()
print('Total time taken: ', end-start)
```

Hope it's useful for you too!  