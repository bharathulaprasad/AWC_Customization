# AWC_Customization



Starting Teamcenter 13, Active workspace introduces Active Architect.
What is Active Architect?
Active Architect is a collection of pages that allows you to:

Easily modify existing command placements, visibility, icons, and so on.

Quickly create your own commands. 

It has mainly two components Gateway and UI Builder.
Gateway:
This is a web application framework that resides between the Active Workspace client application and your browser. It intercepts incoming requests and merges your new and modified content with the main content so you can see your changes without having to rebuild the web application.
UI Builder:
The Active Workspace UI builder consists of several main locations that provide the user interface for dynamic configuration. Dynamic configuration is designed for your development and testing sites, and Siemens Digital Industries Software does not recommend using Active Architect or any other dynamic configuration capabilities in your production environment.
Command Builder

Use this location to dynamically modify declarative command definitions in Active Workspace.

You can search for commands and modify almost all of their attributes — their icon, title, placement, and even the handlers that determine what the command does.

You can see your changes in real time while using developer mode.

Panel Builder

Use this location to dynamically modify declarative command panel definitions in Active Workspace.

Panel Builder is a visual editor that you can use to quickly author declarative panels. It is a WYSIWYG tool where declarative panels can be created and edited using drag-and-drop operations.

Action Builder

Use this location to dynamically modify declarative command action definitions in Active Workspace.

This is a visual editor that you can use to quickly author actions. It is a WYSIWYG tool where success and failure connections are drawn between actions using drag-and-drop operations.

This is repository for experiments made on Teamcenter Active workspace Architect
Requires following components installed in Teamcenter 13.2 and Active workspace 5.2
1. Microservices Framework
2. Command Prediction Service
3. File Repository Service
4. Teamcenter GraphQL Service
5. Active workspace Gateway
6. Active workspace Client
7. Active Architect Core


Activate developer mode by inserting ?dev in the URL.

host:port/?dev

Development scripts
To create custom Active Workspace components, you must work within an environment configured for Active Workspace development. Siemens Digital Industries Software provides several scripts to assist in the development of component modules. Unless otherwise stated, all scripts must be run from the stage directory.

initEnv.cmd
In a Windows environment, run this script to configure the command-line environment variables necessary for Active Workspace development.

awbuild
This script (awbuild.cmd or awbuild.sh) performs both npm run build and npm run publish. It also initializes the command-line environment.

npm run generateModule
This script assists you in creating boilerplate files and directories for individual components. This script does not require any arguments. If you do not provide any, it prompts you to enter the information it requires.

npm run audit
This script checks your declarative definitions against the stated schema version. It reports any errors it encounters, which you must fix before continuing. The current schema file is available in the UI Pattern Library on Support Center.

For example, if a view model file contains "schemaVersion" : "1.0.0", then it will be audited versus schema version.1.0.0, even if 1.0.1 were current.

npm run refresh
This script quick-builds the Active Workspace application locally from STAGE/src and STAGE/repo into STAGE/out/site.

It does not clean first, nor does it perform minification. If you experience any issues with Active Workspace after making changes and performing a refresh, then perform a build instead.

npm run exportToSrc
When you are done making your changes in the UI using Active Architect and you want to commit them, you need to export them into your local source repository.

All of the changes that were made with Command Builder, Panel Builder, and so on, are stored in the declarative artifact service, but any time Active Workspace (the artifact service specifically) is rebuilt, that history and all changes are cleared. Think of exporting back to source as similar to checking in code to source control.

npm run exportToSrc <Gateway Client URL> -- --moduleName=<name of module>

The Gateway Client URL defaults to http://localhost:3000, if not provided.

The name of module is the name of the existing module in which the changes should be stored. It will not create one. You can create a custom module using the generateModule script.
