# ProjectLive Template
This repo is a template for creating projectLive apps. 

# Getting started
The first thing you will want to do it start a repo for your app, using this one as a template. Once you've done that you can start modifying the template code for your app. The template is based on the CSBC version of the app.

# Oauth/synapse login
The app assumes the data to power the visualizations are in synapse, and that the user will be already logged into synapse and has permissions to see the data. The app will create an access token via OAuth and use this to login to synapse and get the needed data. To do this you will need to fill out the file "inst/oauth_config_template.yaml" and rename it "inst/oauth_config.yaml".

For local use you can use an already created oauth client. The information is in last pass, in a folder named "Shared-Sage" in a file named "Synapse Shiny local oauth client config".

For use on shiny server you will need to create your own client, instructions are here: https://help.synapse.org/docs/Using-Synapse-as-an-OAuth-Server.2048327904.html . Once you've created your own client you will have the client secret, client id, and app url to put into the config.

Note, the app uses reticulate and the python client for Synapse, and not the R client.

# Creating the data files
ProjectLive was started using file views that were used to power the NF Synapse portal. Synapse table queries were too slow to use in a shiny app so it was decided to do those beforehand and save the results in RDS files in Synapse. These RDS files are what the current app uses. You will need one for each original fileview. The code that creates these for the current app are in the Data-Raw folder. 

If your app doesn't have the fileviews for a synapse portals table, or you want to pull form them directly in the app, that is possble, but would take some work to modify the app to do so.

# Config files
You will need to chnage the synapse config file: "inst/synapse_module.json" to use the synapse ids for your RDS files. In addition you'll need to change the rest of the "module.json" files in the inst dir for modules you intend to use. The fileview tables will likely have different column names, and you may want to visualize things differently than the current app.

# Using projectlive modules
In "R/app_server.R" the various modules are called like:
```
  projectlive.modules::summary_snapshot_module_server(
    id = "summary_snapshot_ui_1",
    data = data,
    config = shiny::reactive(
      jsonlite::read_json("inst/summary_snapshot_module.json")
    )
  )
```

The app is currentl using all the available modules, but you may not to use them all. Comment out or delete the modules you aren't using. Then do the same in "R/app_ui.R". :

```
shiny::tabPanel(
        "Snapshot",
        projectlive.modules::summary_snapshot_module_ui("summary_snapshot_ui_1"),
        icon = shiny::icon("chart-area")
),
```

