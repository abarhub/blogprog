+++
title = "Calcul la taille des répertoires"
date = "2022-11-13"
description = "Calcul la taille des répertoires"
tags = ["python"]
summary = "Calcul la taille des répertoires"
+++
```python
# This is a sample Python script.
import datetime
import os

import pandas as pd
from io import StringIO

import plotly.express as px

import plotly.graph_objects as go

# pd.DataFrame({'A': [1, 2, 3]})
# # print(f'test: {pd.DataFrame}')
#
# index = pd.date_range("1/1/2000", periods=8)
#
# print(index)


class FileSize:
    def __init__(self, df, filename, date):
        self.df = df
        self.filename = filename
        self.date = date


def parse(file):
    colnames = ['size', 'directory']
    df = pd.read_csv(filepath_or_buffer=file, sep='\t',
                     skipinitialspace=True, names=colnames)

    df3 = df.query('size.str.isnumeric()')
    df3 = df3.astype({'size': 'int64'})
    df4 = df3.sort_values('size')
    filename = os.path.basename(file)
    df4['filename'] = filename
    s = filename
    s = s.removesuffix('.txt')
    s = s.removeprefix('res_')
    d = datetime.datetime.strptime(s, '%Y-%m-%d_%H-%M-%S')
    df4['date'] = d

    f = FileSize(df4, filename, d)
    return f


def regroupe(f, f2, name):
    f.df[name] = 0
    for index, row in f2.df.iterrows():
        dir0 = row['directory']
        tmp = f.df.loc[f.df['directory'] == dir0].index
        # print('tmp', tmp)
        if not tmp.empty:
            # tmp['size2']=row['size']
            # tmp.at[0,'size2']=row['size']
            # print('trouve', tmp, tmp[0])
            # print('tmp', tmp)
            f.df.at[tmp[0], name] = row['size']


def supprimeLignesIdentiques(df, diff):
    # np.where((df['Salary_in_1000']>=100) & (df['Age']< 60) & (df['FT_Team'].str.startswith('S')))
    # df.query('Salary_in_1000 >= 100 & Age < 60 & FT_Team.str.startswith("S").values')
    if diff == 0:
        df3 = df.query('size != size2')
    else:
        # df3 = df.query('((size-size2) >'+diff+') and ')
        # df3 = df.query('(abs(size-size2) >' + str(diff) + ') |  ((size-size2) < -' + str(diff) + ') ')
        df3 = df.query('abs(size-size2) >' + str(diff) + ' ')
    return df3


def main():
    dir = 'dir/'

    f1 = parse(dir + 'res_2022-11-10_15-25-30.txt')
    print(f1.df)

    f2 = parse(dir + 'res_2022-10-31_11-24-46.txt')
    print(f2.df)

    regroupe(f1, f2, 'size2')

    print('df modifie', f1.df)

    diffMax = 1_000_000
    diffMax = 100_000_000

    max = 0
    listX = []
    listY = []
    listY2 = []
    listYdiff = []
    for index, row in f1.df.iterrows():
        diff = abs(row['size'] - row['size2'])
        if (diff > max):
            max = diff
        if diff >= diffMax:
            listX.append(row['directory'])
            listY.append(row['size'])
            listY2.append(row['size2'])
            listYdiff.append(abs(row['size'] - row['size2']))

    print('max', max)

    # fig = px.line(x=listX, y=listY, title="sample figure")
    # print(fig)
    fig = go.Figure()
    # Create and style traces
    fig.add_trace(go.Scatter(x=listX, y=listY, name='val_' + str(f1.date),
                             line=dict(color='firebrick', width=2)))
    fig.add_trace(go.Scatter(x=listX, y=listY2, name='val_' + str(f2.date),
                             line=dict(color='green', width=2)))
    fig.add_trace(go.Scatter(x=listX, y=listY2, name='diff',
                             line=dict(color='blue', width=2)))
    fig.show()


# Press the green button in the gutter to run the script.
if __name__ == '__main__':
    main()
```
                    