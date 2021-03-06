# K-Nearest Neighbor classifier

Implementation of K-NN classifier with three distance metrics:

    1. euclidean
    2. manhattan
    3. cosine

## Example:

    >>> from k_neighbors import K_NN
    >>> clf = K_NN(K=3, metric = 'euclidean')
    >>> X = [[3.4, 0.2], [3.7, 0.4], [3.6, 0.2], [3.3, 0.5], [3.4, 0.2],
    ...      [3.2, 1.8], [2.8, 1.3], [2.5, 1.5], [2.8, 1.2], [2.9, 1.3],
    ...      [3.2, 1.8], [2.8, 1.8], [3.0, 1.8], [2.8, 2.1], [3.0, 1.6]]
    >>> y = [0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 2, 2, 2, 2, 2]
    >>> clf.fit(X, y)
    >>> clf.predict([3.3, 0.4])
    [0]
    >>> clf.predict([3.0, 1.4])
    [1]
    >>> clf.predict([3.2, 1.9])
    [2]
    
    >>> clf.fit(X,y)
    >>> clf.predict([1,4])
    [0]
    >>> clf.predict([4,3])
    [1]
    >>> clf.predict([4,1])
    [2]


k-NN for alphabetical data using feature extraction (one-hot representation):

    >>> train = [['med', 'low', '3', '2', 'small', 'high'],
    ...        ['high', 'low', '5more', 'more', 'med', 'high'],
    ...        ['high', 'med', '4', '4', 'big', 'high'],
    ...        ['high', 'high', '4', 'more', 'big', 'high'],
    ...        ['med', 'high', '2', 'more', 'big', 'high'],
    ...        ['vhigh', 'high', '4', 'more', 'small', 'high'],
    ...        ['med', 'low', '5more', 'more', 'big', 'med'],
    ...        ['high', 'med', '3', '2', 'big', 'low'],
    ...        ['med', 'high', '4', 'more', 'big', 'low'],
    ...        ['high', 'vhigh', '3', '2', 'med', 'med']]
    >>>
    >>> target = ['unacc', 'acc', 'acc', 'acc', 'acc', 'unacc', 'good', 'unacc', 'unacc', 'unacc']
    >>>
    >>> from vectorizer import FeatExtraction
    >>> vec = FeatExtraction()
    >>> vec.fit(train)
    >>>
    >>> test = [['high', 'low', '3', 'more', 'small', 'high'],
    ...  ['high', 'high', '3', 'more', 'med', 'low'],
    ...  ['low', 'low', '2', '2', 'med', 'low'],
    ...  ['vhigh', 'vhigh', '2', '2', 'small', 'med'],
    ...  ['low', 'vhigh', '3', '4', 'small', 'high'],
    ...  ['vhigh', 'med', '2', 'more', 'big', 'high'],
    ...  ['vhigh', 'vhigh', '2', 'more', 'med', 'med'],
    ...  ['low', 'low', '2', '4', 'med', 'low'],
    ...  ['low', 'high', '2', '4', 'small', 'med'],
    ...  ['vhigh', 'med', '2', '2', 'med', 'low']]
    >>>
    >>> vec_train = vec.one_hot(train)
    >>> vec_test = vec.one_hot(test)
    >>>
    >>> vec_train.astype(int)
    array([[0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0],
           [1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 1, 0, 0],
           [1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 1, 0, 0],
           [1, 0, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 1, 0, 0],
           [0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0],
           [0, 0, 1, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0, 1, 0, 0],
           [0, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 1, 0],
           [1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 1],
           [0, 1, 0, 1, 0, 0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 1],
           [1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0]])
    >>>
    >>> vec_test.astype(int)
    array([[1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 0],
           [1, 0, 0, 1, 0, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1],
           [0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1],
           [0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0],
           [0, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0],
           [0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 0, 0, 1, 0, 0, 1, 1, 0, 0],
           [0, 0, 1, 0, 0, 1, 0, 1, 0, 0, 0, 0, 0, 1, 0, 1, 0, 0, 1, 0],
           [0, 0, 0, 0, 0, 0, 1, 1, 0, 0, 0, 0, 1, 0, 0, 1, 0, 0, 0, 1],
           [0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 0, 1, 0, 1, 0, 0, 0, 1, 0],
           [0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1, 0, 0, 0, 1]])
    >>>
    >>> from k_neighbors import K_NN
    >>> clf = K_NN(K=3,metric='cosine')
    >>> clf.fit(vec_train, target)
    >>> 
    >>> clf.predict(vec_test)
    ['acc', 'acc', 'unacc', 'unacc', 'unacc', 'acc', 'acc', 'acc', 'acc', 'unacc']
