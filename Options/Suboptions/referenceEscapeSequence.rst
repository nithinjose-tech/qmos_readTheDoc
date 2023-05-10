Reference Escape Sequence
+++++++++++++++++++++++++

::


    from google.colab import drive
    drive.mount('/content/drive')

*Importing pandas packages*

::

    import pandas as pd

::

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

*Replacing escape sequences like \r \n from the reference summaries in the given dataset and appending in the dictionary created*

::

  for i in range(20):
  if not pd.isna(df.iloc[i][4]):
    str1=df.iloc[i][4].replace('\r',"").replace('\n',"")
  else:
    str1=""
  if not pd.isna(df.iloc[i][5]):
    str2=df.iloc[i][5].replace('\r',"").replace('\n',"")
  else:
    str2=""
  if not pd.isna(df.iloc[i][6]):
    str3=df.iloc[i][6].replace('\r',"").replace('\n',"")
  else:
    str3=""
  if not pd.isna(df.iloc[i][7]):
    str4=df.iloc[i][7].replace('\r',"").replace('\n',"")
  else:
    str4=""
  if not pd.isna(df.iloc[i][8]):
    str5=df.iloc[i][8].replace('\r',"").replace('\n',"")
  else:
    str5=""
  if not pd.isna(df.iloc[i][9]):
    str6=df.iloc[i][9].replace('\r',"").replace('\n',"")
  else:
    str6=""
  


  data['index'].append(df.iloc[i][0])
  data['file'].append(df.iloc[i][1])
  data['doc'].append(df.iloc[i][2])
  data['doc_dump'].append(df.iloc[i][3])
  data['1_200e'].append(str1)
  data['1_400e'].append(str2)
  data['2_200e'].append(str3)
  data['2_400e'].append(str4)
  data['3_200e'].append(str5)
  data['3_400e'].append(str6)



::

  for i in range(20,59):
  if not pd.isna(df.iloc[i][4]):
    str1=df.iloc[i][4].replace('\r',"").replace('\n',"")
  else:
    str1=""
  if not pd.isna(df.iloc[i][5]):
    str2=df.iloc[i][5].replace('\r',"").replace('\n',"")
  else:
    str2=""
  if not pd.isna(df.iloc[i][6]):
    str3=df.iloc[i][6].replace('\r',"").replace('\n',"")
  else:
    str3=""
  if not pd.isna(df.iloc[i][7]):
    str4=df.iloc[i][7].replace('\r',"").replace('\n',"")
  else:
    str4=""
  if not pd.isna(df.iloc[i][8]):
    str5=df.iloc[i][8].replace('\r',"").replace('\n',"")
  else:
    str5=""
  if not pd.isna(df.iloc[i][9]):
    str6=df.iloc[i][9].replace('\r',"").replace('\n',"")
  else:
    str6=""

  data['index'].append(df.iloc[i][0])
  data['file'].append(df.iloc[i][1])
  data['doc'].append(df.iloc[i][2])
  data['doc_dump'].append(df.iloc[i][3])
  data['1_200e'].append(str1)
  data['1_400e'].append(str2)
  data['2_200e'].append(str3)
  data['2_400e'].append(str4)
  data['3_200e'].append(str5)
  data['3_400e'].append(str6)


*Converting the dictionary created to a dataframe*
::

    d = pd.DataFrame.from_dict(data)
    d.set_index('index',inplace = True)
    d.sort_index(ascending=True, inplace=True)

::

    df.head(59)


*Converting the dataframe to csv file*

::

    
    d.to_csv('/content/drive/MyDrive/DUC 2002 E/Input Files/DUC 2002 Extractive.csv')


