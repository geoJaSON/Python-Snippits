## GIS
**Connect to Portal**

    gis = GIS(<portal url>,verify_cert=False)
*or*

    GIS(username="",password="")

**Read a token from file**

    with open('./token.txt') as f:  
         stoken = f.readline()
    gis = GIS(<portal url>, token = stoken)

**Create Token**

    gis._con.token

## Layers
**Import layer as Pandas DF**

    df = flayer.query(as_df=True)

*or*

    df = flayer.query).sdf

*or*

    df = pd.DataFrame.spatial.from_layer(flayer)

**Load feature service**

    layer_item = gis.content.get(<item id>)  
    layers = layer_item.layers  
    flayer = layers[0]  
    fset=flayer.query()  
    features = fset.features  
    tables = layer_item.tables  
    flayer_photos=tables[0]

*or*

    flayer = features.FeatureLayer(<rest endpoint>)
**Query flayer (this example finds related records)**

    for f in features:  
         fset_photos=tables[3].query(where="parentglobalid = '%s'" % (f.attributes['globalid']))  
         features_photos = fset_photos.features

## Features
**Edit a feature**

flayer.edit_features(updates=[{'attributes':{'objectid':f.attributes['objectid'],'field':'value'}}])

**Add a feature**

flayer.edit_features(adds=[{'attributes':{'field':'value','field':'value'}}])

**Download attachments**

    for f in features:  
        attList = flayer.attachments.get_list(oid=f.attributes['objectid'])  
        for att in attList:  
             flayer.attachments.download(f.attributes['objectid'],attachment_id=att['id'],save_path = <folderpath>)

**Add attachment**

    flayer.attachments.add(f.attributes['objectid'], <file>,)

**Datetime object to Esri**

    int(time.mktime((<datetime object>).timetuple())*1000+63200000)

**Esri to Datetime**

    datetime.datetime.fromtimestamp(f.attributes['date']/1000)

**String Date to Esri**

    int(time.mktime(datetime.strptime(str(<string>), "%Y-%m-%d").timetuple()))*1000+63200000

**Push Dataframe to Feature Layer**

    def assemble_funding_updates(row):  
        try:
            edit_feature = {'objectid': funding_keys[str(row['p2_number'])]}
            for col in swd2101.columns:
                edit_feature[col] = row[col]  
            feat = {'attributes': edit_feature}
            updates_to_push.append(feat)
        except KeyError:
            add_feature = {'parentglobalid':p2_keys[str(row['p2_number'])]}  
		    for col in swd2101.columns: 
			    add_feature[col] = row[col]  
		    feat = {'attributes': add_feature} #append object into list  
		    adds_to_push.append(feat) #append object into list  
      
    updates_to_push = [] #Create list of all update objects to push  
    adds_to_push = [] #Create list of all insert objects to push  
    df.apply(lambda row: assemble_funding_updates(row), axis=1) #apply the assumble updates function to DF
    
    update_result = flayer.edit_features(updates=updates_to_push, adds=adds_to_push, rollback_on_failure=False) #Commit the update and insert lists
**Calculate a Field**

    flayer.calculate(where="<query expression>", calc_expression={"field": <field>, "value" :<expression>})

**Get Status of Update Push**

    update_result['updateResults'][0]['success']
**Geocoder**

    def geocode(addressLine):  
	    addressLine = addressLine.replace(' ','%20')  
	    with request.urlopen(r'https://geocode.arcgis.com/arcgis/rest/services/World/GeocodeServer/findAddressCandidates?Address=' + addressLine + '&outFields=*&forStorage=false&f=pjson') as response:  
	    source = response.read()  
	    data = json.loads(source)  
	    y = data['candidates'][0].get("location",{}).get("y")  
	    x = data['candidates'][0].get("location",{}).get("x")  
	    address = data['candidates'][0].get("attributes",{}).get("StAddr")  
	    city = data['candidates'][0].get("attributes",{}).get("City")  
	    state = data['candidates'][0].get("attributes",{}).get("Subregion")  
	    score = data['candidates'][0].get("score",{})  
	    return score, x, y, address, city,state

