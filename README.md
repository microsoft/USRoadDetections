Introduction
-------------------
This data is freely available for download and use and contains 
1. 54,484,737 computer generated roads in all US states except Alaska. 
2. 5,931,242 computer generated roads in all US states except Alaska that are missing in OpenStreetMaps roads drop from 02-May-2020

License
-------------------
This data is licensed by Microsoft under the [Open Data Commons Open Database License (ODbL)](https://opendatacommons.org/licenses/odbl/)

## FAQ
#### What the data include:
1. 54,484,737 computer generated roads in all US states except Alaska. 
2. 5,931,242 computer generated roads in all US states except Alaska that are missing in OpenStreetMaps (OSM) roads drop from 02-May-2020

#### What is the GeoJson format?
GeoJSON is a format for encoding a variety of geographic data structures. 
For Intensive Documentation and Tutorials, Refer to [GeoJson Blog](http://geojson.org/)

#### Creation Details:
The road extraction is done in four stages (first dataset went through two stages and second went through all four):
1.	Semantic Segmentation – Recognizing road pixels on the aerial image using Convolutional Neural Network (CNN).
2.	Geometry Generation - A series of algorithms and processes transforming output of semantic segmentation into roads in geometry format.
3.  Conflation & Cutting - Excluding roads and parts of roads that already exist in the road network (OSM).
4.  Classification - A classifier to filter out low-confidence roads and predict a road type.

### Scheme
![](/images/scheme.png)

#### CNN architecture
Our network was based on UNet and ResNet and the following papers [U-Net] (https://arxiv.org/abs/1505.04597), [Res U-Net] (https://arxiv.org/pdf/1512.03385.pdf), [Res U-Net] (https://arxiv.org/pdf/1711.10684.pdf).
The model was trained on 512x512 images, it is fully-convolutional, meaning that the model can be applied to an image of any size (constrained by GPU memory, 1088x1088 in our case).

#### Training details
The training set consists of 16800 labeled images. Majority of the satellite images cover diverse residential areas in the US. For the sake of good set representation, we have enriched the set with samples from various areas covering mountains, glaciers, forests, deserts, beaches, coasts, etc.
Images in the set are of 1024x1024 pixel size with 1 meter/pixel resolution. The training is done with Keras toolkit.

#### Metrics
These are the intermediate stage metrics we use to track CNN model improvements and they are pixel based. </br> Pixel precision/recall = 83.06%/80.74%

#### Description
Geometry generation consists of the following steps
1. Image postprocessing
2. Thinning
3. Connectivity improvement
4. Graph construction
5. Finalizing road shapes and network quality
6. Stiching road geojsons between neighboring images where needed

#### Metrics
We use APLS metric to evaluate connectivity. It is measured over images with scale 200x200 meters. </br> APLS precision/recall = 77.61%/71.52%

#### Data Vintage
The vintage of the roads depends on the vintage of the underlying imagery. Because Bing Imagery is a composite of multiple sources it is difficult to know the exact dates for individual pieces of data.

#### How good are the data?
The Osm Missing Data went through a final classifier to ensure that the precision is at least 90%.
Here is another measurement with human OSM editors before the final classifier:
| Label         | %     |
| ------------- |:-------------:|
|Roads added without editing|77%|
|Roads added with minor editing|18%|
|Incorrect roads|5%|

#### Will there be more data coming for other geographies?
Yes, we are working on adding more countries. Next targets are South America and Europe

#### Why is the data being released?
Microsoft has a continued interest in supporting a thriving OpenStreetMap ecosystem.

#### Should we import the data into OpenStreetMap?
This dataset was shared with Facebook, owner or RapID - a tool for adding mined roads to OSM.

### External References

<table>
    <thead>
        <tr>
            <th colspan=4>Full drop of all USA mined roads</th>
            <th colspan=4>OSM missing roads (USA 02-May-2020)</th>
        </tr>
		<tr>
            <th>State</th> <th>Number of Roads</th>  <th>Length km</th> <th>Unzipped MB</th>
			<th>State</th> <th>Number of Roads</th>  <th>Length km</th> <th>Unzipped MB</th>
        </tr>
    </thead>
    <tbody>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/USA.zip">USA</a></td><td>54484737</td><td>9308940</td><td>13459</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/USA.zip">USA</a></td><td>5931242</td><td>817761</td><td>2924</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Alabama.zip">Alabama</a></td><td>1030015</td><td>196256</td><td>268</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Alabama.zip">Alabama</a></td><td>169926</td><td>22311</td><td>83</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Arizona.zip">Arizona</a></td><td>1180273</td><td>160617</td><td>263</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Arizona.zip">Arizona</a></td><td>66934</td><td>10377</td><td>32</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Arkansas.zip">Arkansas</a></td><td>767321</td><td>174286</td><td>208</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Arkansas.zip">Arkansas</a></td><td>154038</td><td>26759</td><td>76</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/California.zip">California</a></td><td>4009971</td><td>470500</td><td>889</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/California.zip">California</a></td><td>252553</td><td>29645</td><td>121</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Colorado.zip">Colorado</a></td><td>1082238</td><td>181699</td><td>268</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Colorado.zip">Colorado</a></td><td>76741</td><td>11584</td><td>38</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Connecticut.zip">Connecticut</a></td><td>427923</td><td>51203</td><td>103</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Connecticut.zip">Connecticut</a></td><td>38427</td><td>3154</td><td>18</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Delaware.zip">Delaware</a></td><td>141175</td><td>17592</td><td>32</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Delaware.zip">Delaware</a></td><td>10225</td><td>969</td><td>4</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Florida.zip">Florida</a></td><td>2712701</td><td>346693</td><td>577</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Florida.zip">Florida</a></td><td>147038</td><td>19932</td><td>69</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Georgia.zip">Georgia</a></td><td>1749917</td><td>283913</td><td>437</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Georgia.zip">Georgia</a></td><td>191975</td><td>24302</td><td>94</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Hawaii.zip">Hawaii</a></td><td>137705</td><td>14953</td><td>29</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Hawaii.zip">Hawaii</a></td><td>13962</td><td>1334</td><td>6</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Idaho.zip">Idaho</a></td><td>562235</td><td>114038</td><td>162</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Idaho.zip">Idaho</a></td><td>73548</td><td>11416</td><td>37</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Illinois.zip">Illinois</a></td><td>1840754</td><td>309918</td><td>407</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Illinois.zip">Illinois</a></td><td>174399</td><td>21305</td><td>83</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Indiana.zip">Indiana</a></td><td>1206595</td><td>213000</td><td>276</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Indiana.zip">Indiana</a></td><td>146195</td><td>16725</td><td>69</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Iowa.zip">Iowa</a></td><td>820387</td><td>222015</td><td>203</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Iowa.zip">Iowa</a></td><td>94436</td><td>11551</td><td>44</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Kansas.zip">Kansas</a></td><td>885228</td><td>253328</td><td>219</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Kansas.zip">Kansas</a></td><td>93413</td><td>13423</td><td>43</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Kentucky.zip">Kentucky</a></td><td>965199</td><td>171887</td><td>269</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Kentucky.zip">Kentucky</a></td><td>190964</td><td>24101</td><td>96</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Louisiana.zip">Louisiana</a></td><td>761323</td><td>150911</td><td>187</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Louisiana.zip">Louisiana</a></td><td>127622</td><td>20813</td><td>61</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Maine.zip">Maine</a></td><td>464244</td><td>89907</td><td>140</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Maine.zip">Maine</a></td><td>80845</td><td>12431</td><td>41</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Maryland.zip">Maryland</a></td><td>800548</td><td>88361</td><td>183</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Maryland.zip">Maryland</a></td><td>39237</td><td>3399</td><td>18</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Massachusetts.zip">Massachusetts</a></td><td>758191</td><td>83294</td><td>178</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Massachusetts.zip">Massachusetts</a></td><td>34552</td><td>2758</td><td>16</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Michigan.zip">Michigan</a></td><td>1712266</td><td>279825</td><td>404</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Michigan.zip">Michigan</a></td><td>177966</td><td>19051</td><td>85</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Minnesota.zip">Minnesota</a></td><td>1393249</td><td>296632</td><td>355</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Minnesota.zip">Minnesota</a></td><td>191433</td><td>26747</td><td>94</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Mississippi.zip">Mississippi</a></td><td>671114</td><td>156392</td><td>185</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Mississippi.zip">Mississippi</a></td><td>134654</td><td>22403</td><td>66</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Missouri.zip">Missouri</a></td><td>1300357</td><td>281199</td><td>351</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Missouri.zip">Missouri</a></td><td>153014</td><td>21355</td><td>76</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Montana.zip">Montana</a></td><td>860457</td><td>180023</td><td>249</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Montana.zip">Montana</a></td><td>130533</td><td>24636</td><td>68</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Nebraska.zip">Nebraska</a></td><td>663577</td><td>187192</td><td>171</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Nebraska.zip">Nebraska</a></td><td>47586</td><td>7036</td><td>23</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Nevada.zip">Nevada</a></td><td>463933</td><td>70773</td><td>107</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Nevada.zip">Nevada</a></td><td>28404</td><td>4568</td><td>13</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/NewHampshire.zip">NewHampshire</a></td><td>243910</td><td>38689</td><td>68</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/NewHampshire.zip">NewHampshire</a></td><td>21741</td><td>2122</td><td>10</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/NewJersey.zip">NewJersey</a></td><td>942622</td><td>98892</td><td>210</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/NewJersey.zip">NewJersey</a></td><td>65934</td><td>5681</td><td>31</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/NewMexico.zip">NewMexico</a></td><td>680561</td><td>127638</td><td>168</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/NewMexico.zip">NewMexico</a></td><td>60150</td><td>10509</td><td>29</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/NewYork.zip">NewYork</a></td><td>1584215</td><td>251629</td><td>404</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/NewYork.zip">NewYork</a></td><td>177720</td><td>18849</td><td>87</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/NorthCarolina.zip">NorthCarolina</a></td><td>1769687</td><td>288948</td><td>461</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/NorthCarolina.zip">NorthCarolina</a></td><td>230270</td><td>28538</td><td>113</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/NorthDakota.zip">NorthDakota</a></td><td>581985</td><td>164082</td><td>154</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/NorthDakota.zip">NorthDakota</a></td><td>33947</td><td>4780</td><td>16</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Ohio.zip">Ohio</a></td><td>1795292</td><td>277164</td><td>420</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Ohio.zip">Ohio</a></td><td>193883</td><td>21635</td><td>94</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Oklahoma.zip">Oklahoma</a></td><td>1014493</td><td>239617</td><td>250</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Oklahoma.zip">Oklahoma</a></td><td>129390</td><td>21496</td><td>63</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Oregon.zip">Oregon</a></td><td>1111082</td><td>173778</td><td>302</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Oregon.zip">Oregon</a></td><td>129581</td><td>20241</td><td>67</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Pennsylvania.zip">Pennsylvania</a></td><td>1922526</td><td>286625</td><td>492</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Pennsylvania.zip">Pennsylvania</a></td><td>223364</td><td>27456</td><td>111</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/RhodeIsland.zip">RhodeIsland</a></td><td>126379</td><td>12978</td><td>28</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/RhodeIsland.zip">RhodeIsland</a></td><td>7863</td><td>610</td><td>3</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/SouthCarolina.zip">SouthCarolina</a></td><td>884137</td><td>153987</td><td>228</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/SouthCarolina.zip">SouthCarolina</a></td><td>102010</td><td>13842</td><td>50</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/SouthDakota.zip">SouthDakota</a></td><td>530158</td><td>151645</td><td>140</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/SouthDakota.zip">SouthDakota</a></td><td>69851</td><td>11593</td><td>34</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Tennessee.zip">Tennessee</a></td><td>1231633</td><td>212032</td><td>333</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Tennessee.zip">Tennessee</a></td><td>240815</td><td>34606</td><td>122</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Texas.zip">Texas</a></td><td>4901657</td><td>831644</td><td>1146</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Texas.zip">Texas</a></td><td>521434</td><td>88391</td><td>253</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Utah.zip">Utah</a></td><td>549837</td><td>86304</td><td>133</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Utah.zip">Utah</a></td><td>45061</td><td>7241</td><td>22</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Vermont.zip">Vermont</a></td><td>164249</td><td>32170</td><td>50</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Vermont.zip">Vermont</a></td><td>30386</td><td>3527</td><td>15</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Virginia.zip">Virginia</a></td><td>1466999</td><td>208827</td><td>378</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Virginia.zip">Virginia</a></td><td>108239</td><td>11788</td><td>54</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Washington.zip">Washington</a></td><td>1565086</td><td>209696</td><td>390</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Washington.zip">Washington</a></td><td>158898</td><td>21397</td><td>80</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/WestVirginia.zip">WestVirginia</a></td><td>446393</td><td>85916</td><td>140</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/WestVirginia.zip">WestVirginia</a></td><td>102378</td><td>15400</td><td>53</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Wisconsin.zip">Wisconsin</a></td><td>1231694</td><td>241375</td><td>309</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Wisconsin.zip">Wisconsin</a></td><td>172143</td><td>20430</td><td>83</td></tr>
		<tr><td><a href="https://usaminedroads.blob.core.windows.net/full-roads-set-model25feb2020-geo15oct2019/Wyoming.zip">Wyoming</a></td><td>371246</td><td>88897</td><td>109</td><td><a href="https://usaminedroads.blob.core.windows.net/osm-missing-roads-model25feb2020-geo15oct2019-osm02may2020/Wyoming.zip">Wyoming</a></td><td>65564</td><td>13543</td><td>33</td></tr>
	</tbody>
</table>
<br>
<br>

# Contributing

This project welcomes contributions and suggestions.  Most contributions require you to agree to a
Contributor License Agreement (CLA) declaring that you have the right to, and actually do, grant us
the rights to use your contribution. For details, visit https://cla.opensource.microsoft.com.

When you submit a pull request, a CLA bot will automatically determine whether you need to provide
a CLA and decorate the PR appropriately (e.g., status check, comment). Simply follow the instructions
provided by the bot. You will only need to do this once across all repos using our CLA.

This project has adopted the [Microsoft Open Source Code of Conduct](https://opensource.microsoft.com/codeofconduct/).
For more information see the [Code of Conduct FAQ](https://opensource.microsoft.com/codeofconduct/faq/) or
contact [opencode@microsoft.com](mailto:opencode@microsoft.com) with any additional questions or comments.

# Legal Notices

Microsoft, Windows, Microsoft Azure and/or other Microsoft products and services referenced in the documentation
may be either trademarks or registered trademarks of Microsoft in the United States and/or other countries.
The licenses for this project do not grant you rights to use any Microsoft names, logos, or trademarks.
Microsoft's general trademark guidelines can be found at http://go.microsoft.com/fwlink/?LinkID=254653.

Privacy information can be found at https://privacy.microsoft.com/en-us/

Microsoft and any contributors reserve all other rights, whether under their respective copyrights, patents,
or trademarks, whether by implication, estoppel or otherwise.
