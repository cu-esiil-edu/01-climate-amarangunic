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
import panel as pn
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







<div id='d39bbd8d-2da2-45f6-b8e4-0c1fb2456cfe'>
  <div id="b3d7b191-bfe4-4422-b6f3-52da2d04a8f4" data-root-id="d39bbd8d-2da2-45f6-b8e4-0c1fb2456cfe" style="display: contents;"></div>
</div>
<script type="application/javascript">(function(root) {
  var docs_json = {"fab7133e-b4f4-467c-855d-9b6274b48c4a":{"version":"3.7.3","title":"Bokeh Application","roots":[{"type":"object","name":"panel.models.browser.BrowserInfo","id":"d39bbd8d-2da2-45f6-b8e4-0c1fb2456cfe"},{"type":"object","name":"panel.models.comm_manager.CommManager","id":"5a29b618-203d-4d5a-a35b-5d53bba31b47","attributes":{"plot_id":"d39bbd8d-2da2-45f6-b8e4-0c1fb2456cfe","comm_id":"cfcec62e902249a6af69fb94450f5a76","client_comm_id":"67e32de5f3b34f0b8e993cba9b03434e"}}],"defs":[{"type":"model","name":"ReactiveHTML1"},{"type":"model","name":"FlexBox1","properties":[{"name":"align_content","kind":"Any","default":"flex-start"},{"name":"align_items","kind":"Any","default":"flex-start"},{"name":"flex_direction","kind":"Any","default":"row"},{"name":"flex_wrap","kind":"Any","default":"wrap"},{"name":"gap","kind":"Any","default":""},{"name":"justify_content","kind":"Any","default":"flex-start"}]},{"type":"model","name":"FloatPanel1","properties":[{"name":"config","kind":"Any","default":{"type":"map"}},{"name":"contained","kind":"Any","default":true},{"name":"position","kind":"Any","default":"right-top"},{"name":"offsetx","kind":"Any","default":null},{"name":"offsety","kind":"Any","default":null},{"name":"theme","kind":"Any","default":"primary"},{"name":"status","kind":"Any","default":"normalized"}]},{"type":"model","name":"GridStack1","properties":[{"name":"ncols","kind":"Any","default":null},{"name":"nrows","kind":"Any","default":null},{"name":"allow_resize","kind":"Any","default":true},{"name":"allow_drag","kind":"Any","default":true},{"name":"state","kind":"Any","default":[]}]},{"type":"model","name":"drag1","properties":[{"name":"slider_width","kind":"Any","default":5},{"name":"slider_color","kind":"Any","default":"black"},{"name":"value","kind":"Any","default":50}]},{"type":"model","name":"click1","properties":[{"name":"terminal_output","kind":"Any","default":""},{"name":"debug_name","kind":"Any","default":""},{"name":"clears","kind":"Any","default":0}]},{"type":"model","name":"FastWrapper1","properties":[{"name":"object","kind":"Any","default":null},{"name":"style","kind":"Any","default":null}]},{"type":"model","name":"NotificationArea1","properties":[{"name":"js_events","kind":"Any","default":{"type":"map"}},{"name":"max_notifications","kind":"Any","default":5},{"name":"notifications","kind":"Any","default":[]},{"name":"position","kind":"Any","default":"bottom-right"},{"name":"_clear","kind":"Any","default":0},{"name":"types","kind":"Any","default":[{"type":"map","entries":[["type","warning"],["background","#ffc107"],["icon",{"type":"map","entries":[["className","fas fa-exclamation-triangle"],["tagName","i"],["color","white"]]}]]},{"type":"map","entries":[["type","info"],["background","#007bff"],["icon",{"type":"map","entries":[["className","fas fa-info-circle"],["tagName","i"],["color","white"]]}]]}]}]},{"type":"model","name":"Notification","properties":[{"name":"background","kind":"Any","default":null},{"name":"duration","kind":"Any","default":3000},{"name":"icon","kind":"Any","default":null},{"name":"message","kind":"Any","default":""},{"name":"notification_type","kind":"Any","default":null},{"name":"_rendered","kind":"Any","default":false},{"name":"_destroyed","kind":"Any","default":false}]},{"type":"model","name":"TemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"BootstrapTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"TemplateEditor1","properties":[{"name":"layout","kind":"Any","default":[]}]},{"type":"model","name":"MaterialTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"ReactiveESM1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"JSComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"ReactComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"AnyWidgetComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"request_value1","properties":[{"name":"fill","kind":"Any","default":"none"},{"name":"_synced","kind":"Any","default":null},{"name":"_request_sync","kind":"Any","default":0}]}]}};
  var render_items = [{"docid":"fab7133e-b4f4-467c-855d-9b6274b48c4a","roots":{"d39bbd8d-2da2-45f6-b8e4-0c1fb2456cfe":"b3d7b191-bfe4-4422-b6f3-52da2d04a8f4"},"root_ids":["d39bbd8d-2da2-45f6-b8e4-0c1fb2456cfe"]}];
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



```python
# Upload csv in parsel date
climate_df = pd.read_csv(
    ncei_path,
    parse_dates=['DATE'],
    na_values=['NaN']
)

# Convert temperatures from tenths of °C to °C
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
# print(climate_df.columns)
```


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







<div id='9db95ff1-dccd-4ffa-94c7-9abb5990ba85'>
  <div id="a8104181-193c-48c2-9c8f-6361b61393c5" data-root-id="9db95ff1-dccd-4ffa-94c7-9abb5990ba85" style="display: contents;"></div>
</div>
<script type="application/javascript">(function(root) {
  var docs_json = {"37ed8307-d518-4a54-ad66-fcbbac5252fc":{"version":"3.7.3","title":"Bokeh Application","roots":[{"type":"object","name":"panel.models.browser.BrowserInfo","id":"9db95ff1-dccd-4ffa-94c7-9abb5990ba85"},{"type":"object","name":"panel.models.comm_manager.CommManager","id":"aedde442-1b57-4144-ae5a-ecfa46c3e23e","attributes":{"plot_id":"9db95ff1-dccd-4ffa-94c7-9abb5990ba85","comm_id":"3f7ebbdf001f489383875a0e0725885f","client_comm_id":"b06f383965804bf682bb605eacdb5016"}}],"defs":[{"type":"model","name":"ReactiveHTML1"},{"type":"model","name":"FlexBox1","properties":[{"name":"align_content","kind":"Any","default":"flex-start"},{"name":"align_items","kind":"Any","default":"flex-start"},{"name":"flex_direction","kind":"Any","default":"row"},{"name":"flex_wrap","kind":"Any","default":"wrap"},{"name":"gap","kind":"Any","default":""},{"name":"justify_content","kind":"Any","default":"flex-start"}]},{"type":"model","name":"FloatPanel1","properties":[{"name":"config","kind":"Any","default":{"type":"map"}},{"name":"contained","kind":"Any","default":true},{"name":"position","kind":"Any","default":"right-top"},{"name":"offsetx","kind":"Any","default":null},{"name":"offsety","kind":"Any","default":null},{"name":"theme","kind":"Any","default":"primary"},{"name":"status","kind":"Any","default":"normalized"}]},{"type":"model","name":"GridStack1","properties":[{"name":"ncols","kind":"Any","default":null},{"name":"nrows","kind":"Any","default":null},{"name":"allow_resize","kind":"Any","default":true},{"name":"allow_drag","kind":"Any","default":true},{"name":"state","kind":"Any","default":[]}]},{"type":"model","name":"drag1","properties":[{"name":"slider_width","kind":"Any","default":5},{"name":"slider_color","kind":"Any","default":"black"},{"name":"value","kind":"Any","default":50}]},{"type":"model","name":"click1","properties":[{"name":"terminal_output","kind":"Any","default":""},{"name":"debug_name","kind":"Any","default":""},{"name":"clears","kind":"Any","default":0}]},{"type":"model","name":"FastWrapper1","properties":[{"name":"object","kind":"Any","default":null},{"name":"style","kind":"Any","default":null}]},{"type":"model","name":"NotificationArea1","properties":[{"name":"js_events","kind":"Any","default":{"type":"map"}},{"name":"max_notifications","kind":"Any","default":5},{"name":"notifications","kind":"Any","default":[]},{"name":"position","kind":"Any","default":"bottom-right"},{"name":"_clear","kind":"Any","default":0},{"name":"types","kind":"Any","default":[{"type":"map","entries":[["type","warning"],["background","#ffc107"],["icon",{"type":"map","entries":[["className","fas fa-exclamation-triangle"],["tagName","i"],["color","white"]]}]]},{"type":"map","entries":[["type","info"],["background","#007bff"],["icon",{"type":"map","entries":[["className","fas fa-info-circle"],["tagName","i"],["color","white"]]}]]}]}]},{"type":"model","name":"Notification","properties":[{"name":"background","kind":"Any","default":null},{"name":"duration","kind":"Any","default":3000},{"name":"icon","kind":"Any","default":null},{"name":"message","kind":"Any","default":""},{"name":"notification_type","kind":"Any","default":null},{"name":"_rendered","kind":"Any","default":false},{"name":"_destroyed","kind":"Any","default":false}]},{"type":"model","name":"TemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"BootstrapTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"TemplateEditor1","properties":[{"name":"layout","kind":"Any","default":[]}]},{"type":"model","name":"MaterialTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"ReactiveESM1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"JSComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"ReactComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"AnyWidgetComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"request_value1","properties":[{"name":"fill","kind":"Any","default":"none"},{"name":"_synced","kind":"Any","default":null},{"name":"_request_sync","kind":"Any","default":0}]}]}};
  var render_items = [{"docid":"37ed8307-d518-4a54-ad66-fcbbac5252fc","roots":{"9db95ff1-dccd-4ffa-94c7-9abb5990ba85":"a8104181-193c-48c2-9c8f-6361b61393c5"},"root_ids":["9db95ff1-dccd-4ffa-94c7-9abb5990ba85"]}];
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











<div id='84499396-575f-4fb8-8592-57e8dc56516a'>
  <div id="c2a49006-842c-4dbd-8549-0ea2b9dc4a2c" data-root-id="84499396-575f-4fb8-8592-57e8dc56516a" style="display: contents;"></div>
</div>
<script type="application/javascript">(function(root) {
  var docs_json = {"812dcf76-0f33-4c4b-86dc-bee660940b1a":{"version":"3.7.3","title":"Bokeh Application","roots":[{"type":"object","name":"Row","id":"84499396-575f-4fb8-8592-57e8dc56516a","attributes":{"name":"Row01115","tags":["embedded"],"stylesheets":["\n:host(.pn-loading):before, .pn-loading:before {\n  background-color: #c3c3c3;\n  mask-size: auto calc(min(50%, 400px));\n  -webkit-mask-size: auto calc(min(50%, 400px));\n}",{"type":"object","name":"ImportedStyleSheet","id":"b6ca67dd-1626-45f5-945a-19f618a3888b","attributes":{"url":"https://cdn.holoviz.org/panel/1.7.1/dist/css/loading.css"}},{"type":"object","name":"ImportedStyleSheet","id":"6c46732e-9433-4b13-b7c6-e96eb9c28682","attributes":{"url":"https://cdn.holoviz.org/panel/1.7.1/dist/css/listpanel.css"}},{"type":"object","name":"ImportedStyleSheet","id":"e3ce8929-a09d-44de-b39e-3fb9c07d9d04","attributes":{"url":"https://cdn.holoviz.org/panel/1.7.1/dist/bundled/theme/default.css"}},{"type":"object","name":"ImportedStyleSheet","id":"8b8570f5-8ae1-4e54-b5f2-03102f07fc67","attributes":{"url":"https://cdn.holoviz.org/panel/1.7.1/dist/bundled/theme/native.css"}}],"min_width":800,"margin":0,"sizing_mode":"stretch_width","align":"start","children":[{"type":"object","name":"Spacer","id":"1951c0ec-2afd-4b52-87e1-f58300d0fb1a","attributes":{"name":"HSpacer01122","stylesheets":["\n:host(.pn-loading):before, .pn-loading:before {\n  background-color: #c3c3c3;\n  mask-size: auto calc(min(50%, 400px));\n  -webkit-mask-size: auto calc(min(50%, 400px));\n}",{"id":"b6ca67dd-1626-45f5-945a-19f618a3888b"},{"id":"e3ce8929-a09d-44de-b39e-3fb9c07d9d04"},{"id":"8b8570f5-8ae1-4e54-b5f2-03102f07fc67"}],"min_width":0,"margin":0,"sizing_mode":"stretch_width","align":"start"}},{"type":"object","name":"Figure","id":"5304dd18-07d4-457b-9fcd-f3faf1316eee","attributes":{"width":800,"height":400,"margin":[5,10],"sizing_mode":"fixed","align":"start","x_range":{"type":"object","name":"Range1d","id":"09d24d5a-c9b2-4d50-bfa7-2db4ee321093","attributes":{"tags":[[["YEAR",null]],[]],"start":1942.0,"end":2025.0,"reset_start":1942.0,"reset_end":2025.0}},"y_range":{"type":"object","name":"Range1d","id":"cd855440-ab76-42e5-99eb-eaa1a67a9760","attributes":{"tags":[[["TAVG_C",null]],{"type":"map","entries":[["invert_yaxis",false],["autorange",false]]}],"start":1.6905037878787876,"end":2.8894583333333332,"reset_start":1.6905037878787876,"reset_end":2.8894583333333332}},"x_scale":{"type":"object","name":"LinearScale","id":"975fe2c2-320a-4105-893a-792f8f7f2dc4"},"y_scale":{"type":"object","name":"LinearScale","id":"f0efdb5e-002a-4a0c-9c7f-15f1bfcd3c5b"},"title":{"type":"object","name":"Title","id":"df43b941-fff2-40d6-9d14-afc523307612","attributes":{"text":"Average Annual Temperature in Karachi (\u00b0C)","text_color":"black","text_font_size":"12pt"}},"renderers":[{"type":"object","name":"GlyphRenderer","id":"4610ce90-8d1e-4937-9e3b-51cf0b803e21","attributes":{"data_source":{"type":"object","name":"ColumnDataSource","id":"556d2ab7-d155-4792-b8d7-240ef9bc4ef8","attributes":{"selected":{"type":"object","name":"Selection","id":"a42dab0a-b3a2-4e10-8b99-25353551997d","attributes":{"indices":[],"line_indices":[]}},"selection_policy":{"type":"object","name":"UnionRenderers","id":"f1092c79-4f2c-470a-a2a9-bca2d28ea2dd"},"data":{"type":"map","entries":[["YEAR",{"type":"ndarray","array":{"type":"bytes","data":"lgcAAJcHAACYBwAAmQcAAJoHAACbBwAAnAcAAJ0HAACeBwAAnwcAAKAHAAChBwAAogcAAKMHAACkBwAApQcAAKYHAACnBwAAqAcAAKkHAACqBwAAqwcAAKwHAACtBwAArgcAAK8HAACwBwAAsQcAALIHAACzBwAAtAcAALUHAAC2BwAAtwcAALgHAAC5BwAAugcAALsHAAC8BwAAvQcAAL4HAAC/BwAAwAcAAMEHAADCBwAAwwcAAMQHAADFBwAAxgcAAMcHAADIBwAAyQcAAMoHAADLBwAAzAcAAM0HAADOBwAAzwcAANAHAADRBwAA0gcAANMHAADUBwAA1QcAANYHAADXBwAA2AcAANkHAADaBwAA2wcAANwHAADdBwAA3gcAAN8HAADgBwAA4QcAAOIHAADjBwAA5AcAAOUHAADmBwAA5wcAAOgHAADpBwAA"},"shape":[84],"dtype":"int32","order":"little"}],["TAVG_C",{"type":"ndarray","array":{"type":"bytes","data":"NtBpA52WBUAm7R/2370EQIMoVOCJoARAS7t8eopYBEDX9oI3m6ADQAAAAAAAAPh/AAAAAAAA+H8AAAAAAAD4fwAAAAAAAPh/AAAAAAAA+H8lv1jyi6X8P/ohIWfUKQVAAAAAAAAA+H8AAAAAAAD4fwAAAAAAAPh/7JLKh3G/BED9R/L0Qb0EQAAAAAAAAPh/AAAAAAAA+H8GxKbSkPMEQKRwPQrXwwRAAAAAAAAA+H8AAAAAAAD4fwAAAAAAAPh/AAAAAAAA+H8AAAAAAAD4fwAAAAAAAPh/AAAAAAAA+H8AAAAAAAD4fwAAAAAAAPh/AAAAAAAA+H9Czz+u5YYFQOLTQG6IpAVAjCsYluPrBUCOH6GVlPEEQFMFo5I6AQVAWtxOwEK1BEA5rzU5mPoEQPkG5+f11QRAYCP+NeLvBEAlwsoMB9sEQEEmxQtk0gRAfNotVkF3BEDF3FgAKtoEQNIdurTyqQRAIlFFiLerBECIEBDx8m4EQAfgUBXK8QRAVBun1JVNBUCSFaBzYvMEQArJTs8gywRAbqnrjJh+BUDj2o7s0PUEQAXjlCGXEQVAlKJZYQr2BEAMjw2i7wAFQJAdeKrHvgVAQVvJQufIBUBR0w81/VAGQNdMibo7wwVAIly8zquEBUC39i6+YZQFQHbE1xCNuQVAchZg8xlnBUDuJViyj6YFQJBBM9kaxwVA+OOqLgJHBUBq2tnQQMAFQCubwe/GiQVAG2oyH4gcBUAUA1ez5ekEQAAAAAAAAPh/GejDheA5BUASsMyA/aQFQA+r0UM8lQVA5KjMrQlbBUCaIL67rLcFQEk23ff5ygVA8x/bzK3iBUBgLl1rdw4GQK8r/MZZ4wVAIOKQUMjxBUBc0BZ+8jgGQCfStBoXMQZA"},"shape":[84],"dtype":"float64","order":"little"}]]}}},"view":{"type":"object","name":"CDSView","id":"d1075e97-f5cc-4adb-bc86-4566d6b9c60e","attributes":{"filter":{"type":"object","name":"AllIndices","id":"f87170ad-b441-45ef-943d-dee84a21aede"}}},"glyph":{"type":"object","name":"Line","id":"98da5891-7dd0-4b41-bf98-c575030843bb","attributes":{"tags":["apply_ranges"],"x":{"type":"field","field":"YEAR"},"y":{"type":"field","field":"TAVG_C"},"line_color":"crimson","line_width":3}},"selection_glyph":{"type":"object","name":"Line","id":"fb6d7d47-815d-4bd8-a99a-aaae56b9f19c","attributes":{"tags":["apply_ranges"],"x":{"type":"field","field":"YEAR"},"y":{"type":"field","field":"TAVG_C"},"line_color":"crimson","line_width":3}},"nonselection_glyph":{"type":"object","name":"Line","id":"de36fe7b-6d4b-4e9f-a142-07379e5551f1","attributes":{"tags":["apply_ranges"],"x":{"type":"field","field":"YEAR"},"y":{"type":"field","field":"TAVG_C"},"line_color":"crimson","line_alpha":0.1,"line_width":3}},"muted_glyph":{"type":"object","name":"Line","id":"cdd01de4-b7a1-4176-867a-5c64ddce654f","attributes":{"tags":["apply_ranges"],"x":{"type":"field","field":"YEAR"},"y":{"type":"field","field":"TAVG_C"},"line_color":"crimson","line_alpha":0.2,"line_width":3}}}}],"toolbar":{"type":"object","name":"Toolbar","id":"5a7f147a-8b97-4b22-b5c9-cc4764d4b0db","attributes":{"tools":[{"type":"object","name":"WheelZoomTool","id":"d6703c34-3bd8-47d1-8c26-4e88b1495c47","attributes":{"tags":["hv_created"],"renderers":"auto","zoom_together":"none"}},{"type":"object","name":"HoverTool","id":"a73522cc-b846-4b90-b4a5-653ac5070d6d","attributes":{"tags":["hv_created"],"renderers":[{"id":"4610ce90-8d1e-4937-9e3b-51cf0b803e21"}],"tooltips":[["YEAR","@{YEAR}"],["TAVG_C","@{TAVG_C}"]]}},{"type":"object","name":"SaveTool","id":"fefe727e-21c9-4c15-9f76-d12bceaacd09"},{"type":"object","name":"PanTool","id":"beefa7c3-16ea-4f0f-994a-d51b7fe734fd"},{"type":"object","name":"BoxZoomTool","id":"b3ee093f-93a9-4984-afaf-f665ff465ff7","attributes":{"dimensions":"both","overlay":{"type":"object","name":"BoxAnnotation","id":"84d499c0-1f7a-40ec-8fe2-12c3783ab61e","attributes":{"syncable":false,"line_color":"black","line_alpha":1.0,"line_width":2,"line_dash":[4,4],"fill_color":"lightgrey","fill_alpha":0.5,"level":"overlay","visible":false,"left":{"type":"number","value":"nan"},"right":{"type":"number","value":"nan"},"top":{"type":"number","value":"nan"},"bottom":{"type":"number","value":"nan"},"left_units":"canvas","right_units":"canvas","top_units":"canvas","bottom_units":"canvas","handles":{"type":"object","name":"BoxInteractionHandles","id":"b4086f01-188d-40c7-878e-5391340c15b0","attributes":{"all":{"type":"object","name":"AreaVisuals","id":"39a8a2a3-c986-45d1-961d-3ae29ba2cdab","attributes":{"fill_color":"white","hover_fill_color":"lightgray"}}}}}}}},{"type":"object","name":"ResetTool","id":"c6daa365-400f-400d-8f38-7c5cf68399e5"}],"active_drag":{"id":"beefa7c3-16ea-4f0f-994a-d51b7fe734fd"},"active_scroll":{"id":"d6703c34-3bd8-47d1-8c26-4e88b1495c47"}}},"left":[{"type":"object","name":"LinearAxis","id":"fe34e843-05c5-4903-be3a-083798811230","attributes":{"ticker":{"type":"object","name":"BasicTicker","id":"aaf23ddc-1ac7-4268-851a-8ada771bb17d","attributes":{"mantissas":[1,2,5]}},"formatter":{"type":"object","name":"BasicTickFormatter","id":"0c3297ac-c2bc-400e-9ba7-00cd5266f052"},"axis_label":"Temperature (\u00b0C)","major_label_policy":{"type":"object","name":"AllLabels","id":"28d9e4d5-3709-4602-bc25-f9d358bbe98e"}}}],"below":[{"type":"object","name":"LinearAxis","id":"bdaca7b1-92d7-4f0b-970c-db96f20c3663","attributes":{"ticker":{"type":"object","name":"BasicTicker","id":"a86c1b3e-b239-407c-b89c-f023a6e88d4d","attributes":{"mantissas":[1,2,5]}},"formatter":{"type":"object","name":"BasicTickFormatter","id":"0031d0a6-6c1a-4cc7-a245-4f7ff87fd62d"},"axis_label":"Year","major_label_policy":{"type":"object","name":"AllLabels","id":"610d7c4c-c605-4f40-a0dc-f1f92d1c0260"}}}],"center":[{"type":"object","name":"Grid","id":"d423aed3-269f-487f-8bc0-6480fe5da9f3","attributes":{"axis":{"id":"bdaca7b1-92d7-4f0b-970c-db96f20c3663"},"ticker":{"id":"a86c1b3e-b239-407c-b89c-f023a6e88d4d"}}},{"type":"object","name":"Grid","id":"c77c6913-93dd-4a69-bb46-d8386d62e27d","attributes":{"dimension":1,"axis":{"id":"fe34e843-05c5-4903-be3a-083798811230"},"ticker":{"id":"aaf23ddc-1ac7-4268-851a-8ada771bb17d"}}}],"min_border_top":10,"min_border_bottom":10,"min_border_left":10,"min_border_right":10,"output_backend":"webgl"}},{"type":"object","name":"Spacer","id":"78459630-6225-43be-91e5-c1af03f1941a","attributes":{"name":"HSpacer01123","stylesheets":["\n:host(.pn-loading):before, .pn-loading:before {\n  background-color: #c3c3c3;\n  mask-size: auto calc(min(50%, 400px));\n  -webkit-mask-size: auto calc(min(50%, 400px));\n}",{"id":"b6ca67dd-1626-45f5-945a-19f618a3888b"},{"id":"e3ce8929-a09d-44de-b39e-3fb9c07d9d04"},{"id":"8b8570f5-8ae1-4e54-b5f2-03102f07fc67"}],"min_width":0,"margin":0,"sizing_mode":"stretch_width","align":"start"}}]}}],"defs":[{"type":"model","name":"ReactiveHTML1"},{"type":"model","name":"FlexBox1","properties":[{"name":"align_content","kind":"Any","default":"flex-start"},{"name":"align_items","kind":"Any","default":"flex-start"},{"name":"flex_direction","kind":"Any","default":"row"},{"name":"flex_wrap","kind":"Any","default":"wrap"},{"name":"gap","kind":"Any","default":""},{"name":"justify_content","kind":"Any","default":"flex-start"}]},{"type":"model","name":"FloatPanel1","properties":[{"name":"config","kind":"Any","default":{"type":"map"}},{"name":"contained","kind":"Any","default":true},{"name":"position","kind":"Any","default":"right-top"},{"name":"offsetx","kind":"Any","default":null},{"name":"offsety","kind":"Any","default":null},{"name":"theme","kind":"Any","default":"primary"},{"name":"status","kind":"Any","default":"normalized"}]},{"type":"model","name":"GridStack1","properties":[{"name":"ncols","kind":"Any","default":null},{"name":"nrows","kind":"Any","default":null},{"name":"allow_resize","kind":"Any","default":true},{"name":"allow_drag","kind":"Any","default":true},{"name":"state","kind":"Any","default":[]}]},{"type":"model","name":"drag1","properties":[{"name":"slider_width","kind":"Any","default":5},{"name":"slider_color","kind":"Any","default":"black"},{"name":"value","kind":"Any","default":50}]},{"type":"model","name":"click1","properties":[{"name":"terminal_output","kind":"Any","default":""},{"name":"debug_name","kind":"Any","default":""},{"name":"clears","kind":"Any","default":0}]},{"type":"model","name":"FastWrapper1","properties":[{"name":"object","kind":"Any","default":null},{"name":"style","kind":"Any","default":null}]},{"type":"model","name":"NotificationArea1","properties":[{"name":"js_events","kind":"Any","default":{"type":"map"}},{"name":"max_notifications","kind":"Any","default":5},{"name":"notifications","kind":"Any","default":[]},{"name":"position","kind":"Any","default":"bottom-right"},{"name":"_clear","kind":"Any","default":0},{"name":"types","kind":"Any","default":[{"type":"map","entries":[["type","warning"],["background","#ffc107"],["icon",{"type":"map","entries":[["className","fas fa-exclamation-triangle"],["tagName","i"],["color","white"]]}]]},{"type":"map","entries":[["type","info"],["background","#007bff"],["icon",{"type":"map","entries":[["className","fas fa-info-circle"],["tagName","i"],["color","white"]]}]]}]}]},{"type":"model","name":"Notification","properties":[{"name":"background","kind":"Any","default":null},{"name":"duration","kind":"Any","default":3000},{"name":"icon","kind":"Any","default":null},{"name":"message","kind":"Any","default":""},{"name":"notification_type","kind":"Any","default":null},{"name":"_rendered","kind":"Any","default":false},{"name":"_destroyed","kind":"Any","default":false}]},{"type":"model","name":"TemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"BootstrapTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"TemplateEditor1","properties":[{"name":"layout","kind":"Any","default":[]}]},{"type":"model","name":"MaterialTemplateActions1","properties":[{"name":"open_modal","kind":"Any","default":0},{"name":"close_modal","kind":"Any","default":0}]},{"type":"model","name":"ReactiveESM1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"JSComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"ReactComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"AnyWidgetComponent1","properties":[{"name":"esm_constants","kind":"Any","default":{"type":"map"}}]},{"type":"model","name":"request_value1","properties":[{"name":"fill","kind":"Any","default":"none"},{"name":"_synced","kind":"Any","default":null},{"name":"_request_sync","kind":"Any","default":0}]}]}};
  var render_items = [{"docid":"812dcf76-0f33-4c4b-86dc-bee660940b1a","roots":{"84499396-575f-4fb8-8592-57e8dc56516a":"c2a49006-842c-4dbd-8549-0ea2b9dc4a2c"},"root_ids":["84499396-575f-4fb8-8592-57e8dc56516a"]}];
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



### Observations on the Average Annual Temperature in Karachi, Pakistan

- **There is a general upward trend in average annual temperatures from the 1980s to 2023**  
  This may be linked to global climate change, as well as the urban expansion of Karachi, which contributes to the urban heat island effect and overall temperature increases.

- **There are clear gaps and abrupt jumps in the data, particularly between 1950 and 1970**  
  These anomalies are likely caused by missing or incomplete data, errors in historical data collection, or inconsistencies in temperature recording methods. The sharp drop to around 18 °C followed by a sudden rise in 1950 suggests possible data entry issues or lack of quality control in older datasets.



```python
# Year without data
all_years = pd.Series(range(climate_df_clean['YEAR'].min(), climate_df_clean['YEAR'].max()+1))
years_with_data = climate_df_clean['YEAR'].unique()
years_without_data = all_years[~all_years.isin(anios_con_datos)]
print("Years without data:", years_without_data.tolist())

```

    Years without data: [1947, 1948, 1949, 1950, 1951, 1954, 1955, 1956, 1959, 1960, 1963, 1964, 1965, 1966, 1967, 1968, 1969, 1970, 1971, 1972, 2013]



```python
%%capture
%%bash
jupyter nbconvert climate-Karachi-marangunic.ipynb --to markdown
jupyter nbconvert climate-Karachi-marangunic.ipynb --to html
```

Finally, be sure to `Restart` and `Run all` to make sure your notebook
works all the way through!
