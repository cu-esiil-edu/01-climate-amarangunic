# Climate Coding Challenge

Climate change is impacting the way people live around the world

## There are more Earth Observation data online than any one person could ever look at

[NASA’s Earth Observing System Data and Information System (EOSDIS)
alone manages over 9PB of
data](https://www.earthdata.nasa.gov/learn/articles/getting-petabytes-people-how-eosdis-facilitates-earth-observing-data-discovery-and-use).
1 PB is roughly 100 times the entire Library of Congress (a good
approximation of all the books available in the US). It’s all available
to **you** once you learn how to download what you want.

Here we’re using the NOAA National Centers for Environmental Information
(NCEI) [Access Data
Service](https://www.ncei.noaa.gov/support/access-data-service-api-user-documentation)
application progamming interface (API) to request data from their web
servers. We will be using data collected as part of the Global
Historical Climatology Network daily (GHCNd) from their [Climate Data
Online library](https://www.ncdc.noaa.gov/cdo-web/datasets) program at
NOAA.

For this example we’re requesting [daily summary data in Karachi,
Pakistan (station ID
PKM00041780)](https://www.ncdc.noaa.gov/cdo-web/datasets/GHCND/stations/GHCND:PKM00041780/detail).

<link rel="stylesheet" type="text/css" href="./assets/styles.css"><div class="callout callout-style-default callout-titled callout-response"><div class="callout-header"><div class="callout-icon-container"><i class="callout-icon"></i></div><div class="callout-title-container flex-fill">Research and cite your data</div></div><div class="callout-body-container callout-body"><ol type="1">
<li>Research the <a
href="https://www.ncei.noaa.gov/metadata/geoportal/rest/metadata/item/gov.noaa.ncdc:C00861/html"><strong>Global
Historical Climatology Network - Daily</strong></a> data source.</li>
<li>In the cell below, write a 2-3 sentence description of the data
source.</li>
<li>Include a citation of the data (<strong>HINT:</strong> See the ‘Data
Citation’ tab on the GHCNd overview page).</li>
</ol>
<p>Your description should include:</p>
<ul>
<li>who takes the data</li>
<li>where the data were taken</li>
<li>what the maximum temperature units are</li>
<li>how the data are collected</li>
</ul></div></div>

**YOUR DATA DESCRIPTION AND CITATION HERE** 🛎️

## Access NCEI GHCNd Data from the internet using its API 🖥️ 📡 🖥️

The cell below contains the URL for the data you will use in this part
of the notebook. We created this URL by generating what is called an
**API endpoint** using the NCEI [API
documentation](https://www.ncei.noaa.gov/support/access-data-service-api-user-documentation).

> **What’s an API?**
>
> An **application programming interface** (API) is a way for two or
> more computer programs or components to communicate with each other.
> It is a type of software interface, offering a service to other pieces
> of software ([Wikipedia](https://en.wikipedia.org/wiki/API)).

First things first – you will need to import the `earthpy` library to
help with data management and the `pandas` library to work with tabular
data:


```python
# Import required packages
import holoviews as hv
import hvplot.pandas
import pandas as pd
import earthpy
import earthpy.spatial as es
import earthpy.plot as ep
```


<script type="esms-options">{"shimMode": true}</script><style>*[data-root-id],
*[data-root-id] > * {
  box-sizing: border-box;
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  color: var(--vscode-editor-foreground, var(--jp-ui-font-color1));
}

/* Override VSCode background color */
.cell-output-ipywidget-background:has(
    > .cell-output-ipywidget-background > .lm-Widget > *[data-root-id]
  ),
.cell-output-ipywidget-background:has(> .lm-Widget > *[data-root-id]) {
  background-color: transparent !important;
}
</style>







<div id='p1004'>
  <div id="b6a5a34a-870d-46df-9a1f-5b6606d16358" data-root-id="p1004" style="display: contents;"></div>
</div>
<script type="application/javascript">(function(root) {
  var docs_json = {"c1d60cdf-a2b8-4010-9f9f-a0f37e53c7bb":{"version":"3.7.3","title":"Bokeh Application","roots":[{"type":"object","name":"panel.models.browser.BrowserInfo","id":"p1004"},{"type":"object","name":"panel.models.comm_manager.CommManager","id":"p1005","attributes":{"plot_id":"p1004","comm_id":"c5af0f2cac5f440e8b9c3d26333b193b","client_comm_id":"16eee9d12c7a46d89eea6fdd28bcdaa6"}}],"defs":[{"type":"model","name":"ReactiveHTML1"},{"type":"model","name":"FlexBox1","properties":[{"name":"align_content","kind":"Any","default":"flex-start"},{"name":"align_items","kind":"Any","default":"flex-start"},{"name":"flex_direction","kind":"Any","default":"row"},{"name":"flex_wrap","kind":"Any","default":"wrap"},{"name":"gap","kind":"Any","default":""},{"name":"justify_content","kind":"Any","default":"flex-start"}]},{"type":"model","name":"FloatPanel1","properties":[{"name":"config","kind":"Any","default":{"type":"map"}},{"name":"contained","kind":"Any","default":true},{"name":"position","kind":"Any","default":"right-top"},{"name":"offsetx","kind":"Any","default":null},{"name":"offsety","kind":"Any","default":null},{"name":"theme","kind":"Any","default":"primary"},{"name":"status","kind":"Any","default":"normalized"}]},{"type":"model","name":"GridStack1","properties":[{"name":"ncols","kind":"Any","default":null},{"name":"nrows","kind":"Any","default":null},{"name":"allow_resize","kind":"Any","default":true},{"name":"allow_drag","kind":"Any","default":true},{"name":"state","kind":"Any","default":[]}]},{"type":"model","name":"drag1","properties":[{"name":"slider_width","kind":"Any","default":5},{"name":"slider_color","kind":"Any","default":"black"},{"name":"value","kind":"Any","default":50}]},{"type":"model","name":"click1","properties":[{"name":"terminal_output","kind":"Any","default":""},{"name":"debug_name","kind":"Any","default":""},{"name":"clears","kind":"Any","default":0}]},{"type":"model","name":"FastWrapper1","properties":[{"name":"object","kind":"Any","default":null},{"name":"style","kind":"Any","default":null}]},{"type":"model","name":"NotificationArea1","properties":[{"name":"js_events","kind":"Any","default":{"type":"map"}},{"name":"max_notifications","kind":"Any","default":5},{"name":"notifications","kind":"Any","default":[]},{"name":"position","kind":"Any","default":"bottom-right"},{"name":"_clear","kind":"Any","default":0},{"name":"types","kind":"Any","default":[{"type":"map","entries":[["type","warning"],["background","#ffc107"],["icon",{"type":"map","entries":[["className","fas fa-exclamation-triangle"],["tagName","i"],["color","white"]]}]]},{"type":"map","entries":[["type","info"],["background","#007bff"],["icon",{"type":"map","entries":[["className","fas fa-info-circle"],["tagName","i"],["color","white"]]}]]}]}]},{"type":"model","name":"Notification","properties":[{"name":"background","kind":"Any","default":null},{"name":"duration","kind":"Any","default":3000},{"name":"icon","kind":"Any","default":null},{"name":"message","kind":"Any","default":""},{"name":"notification_type","kind":"Any","default":null},{"name":"_rendered","kind":"Any","default":false},{"name":"_destroyed","kind":"Any","default":false}]},{"type":"model","name":"TemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"BootstrapTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"TemplateEditor1","properties":[{"name":"layout","kind":"Any","default":[]}]},{"type":"model","name":"MaterialTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"ReactiveESM1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"JSComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"ReactComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"AnyWidgetComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"request_value1","properties":[{"name":"fill","kind":"Any","default":"none"},{"name":"_synced","kind":"Any","default":null},{"name":"_request_sync","kind":"Any","default":0}]}]}};
  var render_items = [{"docid":"c1d60cdf-a2b8-4010-9f9f-a0f37e53c7bb","roots":{"p1004":"b6a5a34a-870d-46df-9a1f-5b6606d16358"},"root_ids":["p1004"]}];
  var docs = Object.values(docs_json)
  if (!docs) {
    return
  }
  const py_version = docs[0].version.replace('rc', '-rc.').replace('.dev', '-dev.')
  async function embed_document(root) {
    var Bokeh = get_bokeh(root)
    await Bokeh.embed.embed_items_notebook(docs_json, render_items);
    for (const render_item of render_items) {
      for (const root_id of render_item.root_ids) {
	const id_el = document.getElementById(root_id)
	if (id_el.children.length && id_el.children[0].hasAttribute('data-root-id')) {
	  const root_el = id_el.children[0]
	  root_el.id = root_el.id + '-rendered'
	  for (const child of root_el.children) {
            // Ensure JupyterLab does not capture keyboard shortcuts
            // see: https://jupyterlab.readthedocs.io/en/4.1.x/extension/notebook.html#keyboard-interaction-model
	    child.setAttribute('data-lm-suppress-shortcuts', 'true')
	  }
	}
      }
    }
  }
  function get_bokeh(root) {
    if (root.Bokeh === undefined) {
      return null
    } else if (root.Bokeh.version !== py_version) {
      if (root.Bokeh.versions === undefined || !root.Bokeh.versions.has(py_version)) {
	return null
      }
      return root.Bokeh.versions.get(py_version);
    } else if (root.Bokeh.version === py_version) {
      return root.Bokeh
    }
    return null
  }
  function is_loaded(root) {
    var Bokeh = get_bokeh(root)
    return (Bokeh != null && Bokeh.Panel !== undefined)
  }
  if (is_loaded(root)) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (is_loaded(root)) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
	  var Bokeh = get_bokeh(root)
	  if (Bokeh == null || Bokeh.Panel == null) {
            console.warn("Panel: ERROR: Unable to run Panel code because Bokeh or Panel library is missing");
	  } else {
	    console.warn("Panel: WARNING: Attempting to render but not all required libraries could be resolved.")
	    embed_document(root)
	  }
        }
      }
    }, 25, root)
  }
})(window);</script>


The cell below contains the URL you will use to download climate data.
There are two things to notice about the URL code:

1.  It is surrounded by quotes – that means Python will interpret it as
    a `string`, or text, type, which makes sense for a URL.
2.  The URL is too long to display as one line on most screens. We’ve
    put parentheses around it so that we can easily split it into
    multiple lines by writing two strings – one on each line.

<link rel="stylesheet" type="text/css" href="./assets/styles.css"><div class="callout callout-style-default callout-titled callout-task"><div class="callout-header"><div class="callout-icon-container"><i class="callout-icon"></i></div><div class="callout-title-container flex-fill">Try It: Format your URL for readability</div></div><div class="callout-body-container callout-body"><ol type="1">
<li>Pick an expressive variable name for the URL.</li>
<li>Reformat the URL so that it adheres to the <a
href="https://peps.python.org/pep-0008/#maximum-line-length">79-character
PEP-8 line limit</a>, and so that it is <strong>easy to read</strong>.
If you are using GitHub Codespaces, you should see two vertical lines in
each cell – don’t let your code go past the second line.</li>
<li>Replace ‘DATATYPE’, ‘STATION’, and the start and end dates
‘YYYY-MM-DD’, with the values for the data you want to download.</li>
</ol></div></div>


```python
ncei_karachi_url = ('https://www.ncei.noaa.gov/access/services/data/v1?'
           'dataset=daily-summaries&'
           'dataTypes=TAVG,TMIN,TMAX,PRCP&'
           'stations=PKM00041780&'
           'startDate=1942-05-06&'
           'endDate=2025-07-18&'
           'units=metric')
ncei_karachi_url
```




    'https://www.ncei.noaa.gov/access/services/data/v1?dataset=daily-summaries&dataTypes=TAVG,TMIN,TMAX,PRCP&stations=PKM00041780&startDate=1942-05-06&endDate=2025-07-18&units=metric'




```python
project_dirname = 'ncei_karachi_data'  # Carpeta donde se guardarán los datos
ncei_filename = 'karachi_climate_1942_2025.csv'
```

## Download and get started working with NCEI data

Go ahead and use `earthpy` to download data from your API URL. You could
also use Python, but using earthpy saves a file and lets you work
offline later on. If you didn’t already, you should import the `earthpy`
library **at the top of this notebook** so that others who want to use
your code can find it easily.


```python
project = earthpy.Project(dirname=project_dirname)
project.get_data(url=ncei_karachi_url, filename=ncei_filename)
ncei_path = project.project_dir / ncei_filename

# Load the data into a DataFrame
climate_df = pd.read_csv(ncei_path, parse_dates=['DATE'])
```

    
    **Final Configuration Loaded:**
    {}
    Found 'data_home' in environment variables.


    [('https://www.ncei.noaa.gov/access/services/data/v1?dataset=daily-summaries&dataTypes=TAVG,TMIN,TMAX,PRCP&stations=PKM00041780&startDate=1942-05-06&endDate=2025-07-18&units=metric', 'karachi_climate_1942_2025.csv', 'file')]
    karachi_climate_1942_2025.csv
    [PosixPath('/workspaces/data/ncei_karachi_data/karachi_climate_1942_2025.csv')]



```python
# 1. Cargar el CSV con la fecha parseada
climate_df = pd.read_csv(
    ncei_path,
    parse_dates=['DATE'],
    na_values=['NaN']
)

# 2. Convertir temperaturas desde décimas de °C a °C
climate_df['TAVG_C'] = climate_df['TAVG'] / 10
climate_df['TMIN_C'] = climate_df['TMIN'] / 10
climate_df['TMAX_C'] = climate_df['TMAX'] / 10


climate_df['PRCP_mm'] = climate_df['PRCP'] / 10

climate_df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>STATION</th>
      <th>DATE</th>
      <th>PRCP</th>
      <th>TAVG</th>
      <th>TMAX</th>
      <th>TMIN</th>
      <th>TAVG_C</th>
      <th>TMIN_C</th>
      <th>TMAX_C</th>
      <th>PRCP_mm</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>PKM00041780</td>
      <td>1942-05-06</td>
      <td>NaN</td>
      <td>32.1</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>3.21</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>1</th>
      <td>PKM00041780</td>
      <td>1942-05-07</td>
      <td>0.0</td>
      <td>29.6</td>
      <td>32.4</td>
      <td>NaN</td>
      <td>2.96</td>
      <td>NaN</td>
      <td>3.24</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>PKM00041780</td>
      <td>1942-05-08</td>
      <td>0.0</td>
      <td>30.5</td>
      <td>33.0</td>
      <td>28.0</td>
      <td>3.05</td>
      <td>2.8</td>
      <td>3.30</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>PKM00041780</td>
      <td>1942-05-09</td>
      <td>0.0</td>
      <td>30.2</td>
      <td>32.4</td>
      <td>28.0</td>
      <td>3.02</td>
      <td>2.8</td>
      <td>3.24</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>PKM00041780</td>
      <td>1942-05-10</td>
      <td>0.0</td>
      <td>29.9</td>
      <td>31.9</td>
      <td>28.0</td>
      <td>2.99</td>
      <td>2.8</td>
      <td>3.19</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
</div>



# STEP -1: Wrap up

Don’t forget to store your variables so you can use them in other
notebooks! Replace `var1` and `var2` with the variable you want to save,
separated by spaces.


```python
%store climate_df
%store ncei_path
%store project_dirname
%store ncei_filename
```

    Stored 'climate_df' (DataFrame)
    Stored 'ncei_path' (PosixPath)
    Stored 'project_dirname' (str)
    Stored 'ncei_filename' (str)



```python
import panel as pn
```


```python
print(climate_df.columns)
```

    Index(['STATION', 'DATE', 'PRCP', 'TAVG', 'TMAX', 'TMIN', 'TAVG_C', 'TMIN_C',
           'TMAX_C', 'PRCP_mm'],
          dtype='object')



```python
import pandas as pd
import hvplot.pandas
import panel as pn

pn.extension()

# Asegurarte de que la columna DATE esté en formato datetime
climate_df['DATE'] = pd.to_datetime(climate_df['DATE'])

# Filtrar datos válidos
climate_df_clean = climate_df[climate_df['TAVG_C'].notna()].copy()
climate_df_clean['YEAR'] = climate_df_clean['DATE'].dt.year

# Calcular promedio anual solo para años con datos
annual_avg = climate_df_clean.groupby('YEAR')['TAVG_C'].mean().reset_index()

# Crear un rango completo de años desde el primero al último
year_range = pd.DataFrame({'YEAR': range(climate_df_clean['YEAR'].min(), climate_df_clean['YEAR'].max() + 1)})

# Hacer merge para introducir NaN en los años sin datos
annual_avg_full = year_range.merge(annual_avg, on='YEAR', how='left')

# Graficar
temp_plot = annual_avg_full.hvplot.line(
    x='YEAR',
    y='TAVG_C',
    title='Average Annual Temperature in Karachi (°C)',
    xlabel='Year',
    ylabel='Temperature (°C)',
    width=800,
    height=400,
    line_width=3,
    color='crimson',
    grid=True,
    hover=True
)
# Mostrar gráfico
temp_plot
# (opcional) Guardar como archivo HTML
#hvplot.save(temp_plot, 'karachi_avg_temp_with_gaps.html')
```


<script type="esms-options">{"shimMode": true}</script><style>*[data-root-id],
*[data-root-id] > * {
  box-sizing: border-box;
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  color: var(--vscode-editor-foreground, var(--jp-ui-font-color1));
}

/* Override VSCode background color */
.cell-output-ipywidget-background:has(
    > .cell-output-ipywidget-background > .lm-Widget > *[data-root-id]
  ),
.cell-output-ipywidget-background:has(> .lm-Widget > *[data-root-id]) {
  background-color: transparent !important;
}
</style>







<div id='p1006'>
  <div id="c9573ea2-09a0-405a-b01a-9969f1ddf973" data-root-id="p1006" style="display: contents;"></div>
</div>
<script type="application/javascript">(function(root) {
  var docs_json = {"571fa8de-3488-4ddc-bab6-023898a8049c":{"version":"3.7.3","title":"Bokeh Application","roots":[{"type":"object","name":"panel.models.browser.BrowserInfo","id":"p1006"},{"type":"object","name":"panel.models.comm_manager.CommManager","id":"p1007","attributes":{"plot_id":"p1006","comm_id":"c6fa394fd58d499abf80f9af68b9e22e","client_comm_id":"5f7219f5808d4ce59c4c2b14d048e1fe"}}],"defs":[{"type":"model","name":"ReactiveHTML1"},{"type":"model","name":"FlexBox1","properties":[{"name":"align_content","kind":"Any","default":"flex-start"},{"name":"align_items","kind":"Any","default":"flex-start"},{"name":"flex_direction","kind":"Any","default":"row"},{"name":"flex_wrap","kind":"Any","default":"wrap"},{"name":"gap","kind":"Any","default":""},{"name":"justify_content","kind":"Any","default":"flex-start"}]},{"type":"model","name":"FloatPanel1","properties":[{"name":"config","kind":"Any","default":{"type":"map"}},{"name":"contained","kind":"Any","default":true},{"name":"position","kind":"Any","default":"right-top"},{"name":"offsetx","kind":"Any","default":null},{"name":"offsety","kind":"Any","default":null},{"name":"theme","kind":"Any","default":"primary"},{"name":"status","kind":"Any","default":"normalized"}]},{"type":"model","name":"GridStack1","properties":[{"name":"ncols","kind":"Any","default":null},{"name":"nrows","kind":"Any","default":null},{"name":"allow_resize","kind":"Any","default":true},{"name":"allow_drag","kind":"Any","default":true},{"name":"state","kind":"Any","default":[]}]},{"type":"model","name":"drag1","properties":[{"name":"slider_width","kind":"Any","default":5},{"name":"slider_color","kind":"Any","default":"black"},{"name":"value","kind":"Any","default":50}]},{"type":"model","name":"click1","properties":[{"name":"terminal_output","kind":"Any","default":""},{"name":"debug_name","kind":"Any","default":""},{"name":"clears","kind":"Any","default":0}]},{"type":"model","name":"FastWrapper1","properties":[{"name":"object","kind":"Any","default":null},{"name":"style","kind":"Any","default":null}]},{"type":"model","name":"NotificationArea1","properties":[{"name":"js_events","kind":"Any","default":{"type":"map"}},{"name":"max_notifications","kind":"Any","default":5},{"name":"notifications","kind":"Any","default":[]},{"name":"position","kind":"Any","default":"bottom-right"},{"name":"_clear","kind":"Any","default":0},{"name":"types","kind":"Any","default":[{"type":"map","entries":[["type","warning"],["background","#ffc107"],["icon",{"type":"map","entries":[["className","fas fa-exclamation-triangle"],["tagName","i"],["color","white"]]}]]},{"type":"map","entries":[["type","info"],["background","#007bff"],["icon",{"type":"map","entries":[["className","fas fa-info-circle"],["tagName","i"],["color","white"]]}]]}]}]},{"type":"model","name":"Notification","properties":[{"name":"background","kind":"Any","default":null},{"name":"duration","kind":"Any","default":3000},{"name":"icon","kind":"Any","default":null},{"name":"message","kind":"Any","default":""},{"name":"notification_type","kind":"Any","default":null},{"name":"_rendered","kind":"Any","default":false},{"name":"_destroyed","kind":"Any","default":false}]},{"type":"model","name":"TemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"BootstrapTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"TemplateEditor1","properties":[{"name":"layout","kind":"Any","default":[]}]},{"type":"model","name":"MaterialTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"ReactiveESM1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"JSComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"ReactComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"AnyWidgetComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"request_value1","properties":[{"name":"fill","kind":"Any","default":"none"},{"name":"_synced","kind":"Any","default":null},{"name":"_request_sync","kind":"Any","default":0}]}]}};
  var render_items = [{"docid":"571fa8de-3488-4ddc-bab6-023898a8049c","roots":{"p1006":"c9573ea2-09a0-405a-b01a-9969f1ddf973"},"root_ids":["p1006"]}];
  var docs = Object.values(docs_json)
  if (!docs) {
    return
  }
  const py_version = docs[0].version.replace('rc', '-rc.').replace('.dev', '-dev.')
  async function embed_document(root) {
    var Bokeh = get_bokeh(root)
    await Bokeh.embed.embed_items_notebook(docs_json, render_items);
    for (const render_item of render_items) {
      for (const root_id of render_item.root_ids) {
	const id_el = document.getElementById(root_id)
	if (id_el.children.length && id_el.children[0].hasAttribute('data-root-id')) {
	  const root_el = id_el.children[0]
	  root_el.id = root_el.id + '-rendered'
	  for (const child of root_el.children) {
            // Ensure JupyterLab does not capture keyboard shortcuts
            // see: https://jupyterlab.readthedocs.io/en/4.1.x/extension/notebook.html#keyboard-interaction-model
	    child.setAttribute('data-lm-suppress-shortcuts', 'true')
	  }
	}
      }
    }
  }
  function get_bokeh(root) {
    if (root.Bokeh === undefined) {
      return null
    } else if (root.Bokeh.version !== py_version) {
      if (root.Bokeh.versions === undefined || !root.Bokeh.versions.has(py_version)) {
	return null
      }
      return root.Bokeh.versions.get(py_version);
    } else if (root.Bokeh.version === py_version) {
      return root.Bokeh
    }
    return null
  }
  function is_loaded(root) {
    var Bokeh = get_bokeh(root)
    return (Bokeh != null && Bokeh.Panel !== undefined)
  }
  if (is_loaded(root)) {
    embed_document(root);
  } else {
    var attempts = 0;
    var timer = setInterval(function(root) {
      if (is_loaded(root)) {
        clearInterval(timer);
        embed_document(root);
      } else if (document.readyState == "complete") {
        attempts++;
        if (attempts > 200) {
          clearInterval(timer);
	  var Bokeh = get_bokeh(root)
	  if (Bokeh == null || Bokeh.Panel == null) {
            console.warn("Panel: ERROR: Unable to run Panel code because Bokeh or Panel library is missing");
	  } else {
	    console.warn("Panel: WARNING: Attempting to render but not all required libraries could be resolved.")
	    embed_document(root)
	  }
        }
      }
    }, 25, root)
  }
})(window);</script>



<script type="esms-options">{"shimMode": true}</script><style>*[data-root-id],
*[data-root-id] > * {
  box-sizing: border-box;
  font-family: var(--jp-ui-font-family);
  font-size: var(--jp-ui-font-size1);
  color: var(--vscode-editor-foreground, var(--jp-ui-font-color1));
}

/* Override VSCode background color */
.cell-output-ipywidget-background:has(
    > .cell-output-ipywidget-background > .lm-Widget > *[data-root-id]
  ),
.cell-output-ipywidget-background:has(> .lm-Widget > *[data-root-id]) {
  background-color: transparent !important;
}
</style>







```python
# Ver años faltantes
todos_los_anios = pd.Series(range(climate_df_clean['YEAR'].min(), climate_df_clean['YEAR'].max()+1))
anios_con_datos = climate_df_clean['YEAR'].unique()
anios_faltantes = todos_los_anios[~todos_los_anios.isin(anios_con_datos)]
print("Años sin datos:", anios_faltantes.tolist())

```

    Años sin datos: [1947, 1948, 1949, 1950, 1951, 1954, 1955, 1956, 1959, 1960, 1963, 1964, 1965, 1966, 1967, 1968, 1969, 1970, 1971, 1972, 2013]



```python
!ls

```

    climate-31-overview.ipynb  climate-40-wrapup.ipynb
    climate-32-wrangle.ipynb   climate-Karachi-marangunic.ipynb
    climate-33-units.ipynb	   karachi_avg_temp_with_gaps.html
    climate-34-plot.ipynb	   karachi_temp_plot.html



```python
%%capture
%%bash
jupyter nbconvert climate-Karachi-marangunic.ipynb --to markdown
```


    ---------------------------------------------------------------------------

    CalledProcessError                        Traceback (most recent call last)

    Cell In[16], line 1
    ----> 1 get_ipython().run_cell_magic('bash', '', '!jupyter nbconvert climate-Karachi-marangunic.ipynb --to markdown\n')


    File /opt/conda/lib/python3.11/site-packages/IPython/core/interactiveshell.py:2549, in InteractiveShell.run_cell_magic(self, magic_name, line, cell)
       2547 with self.builtin_trap:
       2548     args = (magic_arg_s, cell)
    -> 2549     result = fn(*args, **kwargs)
       2551 # The code below prevents the output from being displayed
       2552 # when using magics with decorator @output_can_be_silenced
       2553 # when the last Python token in the expression is a ';'.
       2554 if getattr(fn, magic.MAGIC_OUTPUT_CAN_BE_SILENCED, False):


    File /opt/conda/lib/python3.11/site-packages/IPython/core/magics/script.py:159, in ScriptMagics._make_script_magic.<locals>.named_script_magic(line, cell)
        157 else:
        158     line = script
    --> 159 return self.shebang(line, cell)


    File /opt/conda/lib/python3.11/site-packages/IPython/core/magics/script.py:336, in ScriptMagics.shebang(self, line, cell)
        331 if args.raise_error and p.returncode != 0:
        332     # If we get here and p.returncode is still None, we must have
        333     # killed it but not yet seen its return code. We don't wait for it,
        334     # in case it's stuck in uninterruptible sleep. -9 = SIGKILL
        335     rc = p.returncode or -9
    --> 336     raise CalledProcessError(rc, cell)


    CalledProcessError: Command 'b'!jupyter nbconvert climate-Karachi-marangunic.ipynb --to markdown\n'' returned non-zero exit status 127.


Finally, be sure to `Restart` and `Run all` to make sure your notebook
works all the way through!
