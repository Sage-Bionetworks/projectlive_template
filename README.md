# ProjectLive Template
This repo is a template for creating projectLive apps. 

# Getting started
The first thing you will want to do it start a repo for your app, using this one as a template. Once you've doen that you can start modifying the template code for your app. The template is based on the CSBC version of the app.

# Oauth/synapse login.
The current app assumes the data to power the visualizations are in synapse, and that the user will be already logged into synapse and has permissions to see the data. The app will create an access token via OAuth and use this to login to synapse and get the needed data. To do this you will need to fill out the file "inst/oauth_config_template.yaml" and rename it "inst/oauth_config.yaml".

For local use you can use an already created oauth client. The information is in last pass, in a folder named "Shared-Sage" in a file named "Synapse Shiny local oauth client config".

For use on shiny server you will need to create your own client, instructiosn are here: https://help.synapse.org/docs/Using-Synapse-as-an-OAuth-Server.2048327904.html . Once you've created your own client you will have the client secret id and app url to put into the config.

