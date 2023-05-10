Lemmatization
+++++++++++++

::


    from google.colab import drive
    drive.mount('/content/drive')

*Importing pandas packages*

::

    import pandas as pd

::

    df=pd.read_csv('/content/drive/MyDrive/DUC 2002 E/Input Files/CSW.csv')


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


*Import package for lemmatization*

::

    import nltk
    nltk.download('wordnet')
    nltk.download('omw-1.4')
    from nltk.stem import WordNetLemmatizer 
    lemma=WordNetLemmatizer()

*Lemmatize each word in the data to be summarized*

::

  for i in range(20):
  str=df.iloc[i][2]
  str1=""

  wd=""
  for word in str.split():
    p=""
    if word.endswith('.'):
      p=p+"."
      wd=word.replace(".","")
    elif word.endswith(','):
      p=p+","
      wd=word.replace(",","")
    elif word.endswith('?'):
      p=p+"?"
      wd=word.replace("?","")
    elif word.endswith('!'):
      p=p+"!"
      wd=word.replace("!","")
    elif word.endswith(')'):
      p=p+")"
      wd=word.replace(")","")
    else:
      p=""
      wd=word
    

    w=lemma.lemmatize(wd)
    str1=str1+w+p+" "
  data['index'].append(df.iloc[i][0])
  data['file'].append(df.iloc[i][1])
  data['doc'].append(str1)
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
  str1=""

  wd=""
  for word in str.split():
    p=""
    if word.endswith('.'):
      p=p+"."
      wd=word.replace(".","")
    elif word.endswith(','):
      p=p+","
      wd=word.replace(",","")
    elif word.endswith('?'):
      p=p+"?"
      wd=word.replace("?","")
    elif word.endswith('!'):
      p=p+"!"
      wd=word.replace("!","")
    elif word.endswith(')'):
      p=p+")"
      wd=word.replace(")","")
    else:
      p=""
      wd=word
    

    w=lemma.lemmatize(wd)
    str1=str1+w+p+" "
  data['index'].append(df.iloc[i][0])
  data['file'].append(df.iloc[i][1])
  data['doc'].append(str1)
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

*Converting the dataframe to csv file*

::

    d.to_csv('/content/drive/MyDrive/DUC 2002 E/Input Files/CSW_L.csv')

