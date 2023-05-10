StopWords_v3
++++++++++++

::

    from google.colab import drive
    drive.mount('/content/drive')

*Import stop word package that is a combination of the previously created custom package and NLTK package*

::

    !cp /content/drive/MyDrive/Colab\ Notebooks/stopwords_v2.py /content

::

    import stopwords_v2 as s
    list_swords=s.swords().copy()
    
*Import pandas package*

::

    import pandas as pd

    df=pd.read_csv('/content/drive/MyDrive/DUC 2002 E/Input Files/DUC 2002 Extractive.csv')

*Creating a dictionary to update the changes made to the dataset*

::

    data={'index':[],
        'file':[],
        'doc':[],
        'doc_dump':[],
        '1_200e':[],
        '1_400e':[],
        '2_200e':[],
        '2_400e':[],
        '3_200e':[],
        '3_400e':[]   
    }

*Removing Stopwords from the data*

::

    for i in range(20):
    str=df.iloc[i][2]


    for word in list_swords:
        w=" "+word+" "
        q=" "+word+","
        str=str.replace(w," ")
    data['index'].append(df.iloc[i][0])
    data['file'].append(df.iloc[i][1])
    data['doc'].append(str)
    data['doc_dump'].append(df.iloc[i][3])
    data['1_200e'].append(df.iloc[i][4])
    data['1_400e'].append(df.iloc[i][5])
    data['2_200e'].append(df.iloc[i][6])
    data['2_400e'].append(df.iloc[i][7])
    data['3_200e'].append(df.iloc[i][8])
    data['3_400e'].append(df.iloc[i][9])

::

    for i in range(20,59):
    str=df.iloc[i][2]

    for word in list_swords:
        w=" "+word+" "
        q=" "+word+","
        str=str.replace(w," ")

    data['index'].append(df.iloc[i][0])
    data['file'].append(df.iloc[i][1])
    data['doc'].append(str)
    data['doc_dump'].append(df.iloc[i][3])
    data['1_200e'].append(df.iloc[i][4])
    data['1_400e'].append(df.iloc[i][5])
    data['2_200e'].append(df.iloc[i][6])
    data['2_400e'].append(df.iloc[i][7])
    data['3_200e'].append(df.iloc[i][8])
    data['3_400e'].append(df.iloc[i][9])

*Converting the dictionary created to a dataframe*

::

    d = pd.DataFrame.from_dict(data)
    d.set_index('index',inplace = True)
    d.sort_index(ascending=True, inplace=True)

::

    d.head(-5)

*Converting the dataframe to csv file*

::

    d.to_csv('/content/drive/MyDrive/DUC 2002 E/Input Files/CSW.csv')