## Dataframes

Read XLS

    df = pd.read_excel (<xls>,<sheetname>,keep_default_na=True)

Read CSV

    df = pd.read_csv (<xls>,<sheetname>,keep_default_na=True)

Feature Class To Dataframe

    sdf = pd.DataFrame.spatial.from_featureclass("path\to\your\data\census_example\cities.shp")

Feature Class From Dataframe

    sdf.spatial.to_featureclass(location=r"c:\output_examples\census.shp", overwrite=True)

Dataframe to Spatial DF

    sedf = pd.DataFrame.spatial.from_xy(df=df, x_column='LONGITUDE', y_column='LATITUDE', sr=4326)

Spatial Dataframe to Table

    sub_df.spatial.to_table(location="./sedf_data/cities/cities_table_export.csv", overwrite=True)

Export DF to csv

    df.to_csv(r<path and name of csv>)

Create DF

    df = pd.DataFrame(columns = ['Name','Name'])

Create DF with rows

    df = pd.DataFrame(index=[<list>], columns=[<columns>])

Set index column

    df = df.set_index(<column>)
Query DF

    df_query = df.query(<expression>)
Filter DF

    new_df = df[~df[<field>].isin([<value>])]
Merge 2 DFs

    df = pd.merge(df1, df2, on=<key field>)
Replace in DF

    df[<field>]=df[<field>].str.replace(<old value>,<new value>)

Reset index

    df.reset_index(inplace=True)

Sort DF

    df=df.sort_values(<field>)
## Rows
Show all rows

    pd.set_option('display.max_rows', None)

Show First N Rows

    df = df.head(<n>)
Update cell

    df.at[<row>,<column>] = <value>
Iterate rows

    for index, row in df.iterrows():

Fill Null Cells with 0

    df = df.fillna(0)

Drop Rows with Null Fields    

    df = df.dropna(subset=[<fields>])
## Columns

Convert column to float

    df["storage"] = pd.to_numeric(df["storage"], downcast="float")
Get Max or Min

    df_Max = df1.groupby(<field>).max() or .min()
Group and count

    df.groupby('name')['activity'].value_counts()

Count records in DF by date

    new_df = df[<date field>].groupby(df[<same field>].dt.to_period('D')).count()

Datetime column to Esri date

    df[<column>] = pd.to_datetime(df[<column>]).astype(np.int64)/1e6

Drop Columns

    df =df.drop(columns =[<column names>])

Mass Rename Columns

    df = df.rename({dictionary of old:new}, axis=1)

Rearrange Columns

    df = df[["C", "A", "B"]]

Show all columns

    pd.set_option('display.max_columns', None)

Count unique values

    df.groupby('column')['objectid'].nunique()

Group and Count by Date

    sdf['objectid'].groupby(sdf['paiddate'].dt.to_period('d')).count()

## Display

Format Columns

     df.head(10).style.format({"BasePay": "${:20,.0f}",
    "JobTitle": lambda x:x.lower()})
    .hide_index()\
    .background_gradient(cmap='Blues')
    .bar(subset=["OtherPay",], color='lightgreen')\
    .applymap(lambda x: f”color: {‘red’ if isinstance(x,str) else ‘black’}”)

    def cell_color(value):
         if value < 11:
              color = 'red'
              elif value > 13:
              color = 'yellow'
         else:
              color = 'white'
         return 'color: %s' % color
    new_df.style.bar(subset=["Value"], color='black').applymap(cell_color, subset=['Value'])

Show Graph

    df.plot(<x column>,<y column>,kind='scatter',title='')
    df.plot.area df.plot.barh df.plot.density df.plot.hist df.plot.line df.plot.scatter
    df.plot.bar df.plot.box df.plot.hexbin df.plot.kde df.plot.pie

Show Progress bar (Jupyter)

    from tqdm.notebook import tqdm_notebook
    tqdm_notebook.pandas()
    for n in tqdm(<loop>):

In Line Print for Loop

    print(str(index+1)+"/"+str(len(df)), end = "\r")

## Spatial
Create Buffer Geometry

    sedf['buffer_2'] = sedf.SHAPE.geom.buffer(distance=2)

Get Area

    sedf.buffer_2.geom.area

Get Distance

    sedf.SHAPE.geom.distance_to(sedf.SHAPE[0])

df.spatial.plot(m1)

    sdf.spatial.plot(<map object>)

Google Geocode (<25k per month)

    from geopy.geocoders import GoogleV3
    geolocator = GoogleV3(api_key="")
    <colum or value> = geolocator.geocode(<column or value>)
    df['lat'] = [g.latitude for g in df.gcode]
    df['long'] = [g.longitude for g in df.gcode]

Photon Geocode (free but less accurate)

    from geopy.geocoders import Photon
    geolocator = Photon()
    location = geolocator.geocode("2700 Gulf Freeway, Texas City")
    print(location.latitude, location.longitude)
