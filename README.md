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
8. Active Architect -> UI Builder

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

initEnv
npm run exportToSrc  **<Gateway Client URL>** -- --moduleName=<name of module>

The Gateway Client URL defaults to http://localhost:3000, if not provided.

The name of module is the name of the existing module in which the changes should be stored. It will not create one. You can create a custom module using the generateModule script.


**Now some Technical terms:******Definitions::****  
  
**The stage directory**
Like many JavaScript applications, Active Workspace uses npm to manage dependencies and other build tooling. The primary files related to npm are the package.json file and the node_modules folder.
  


Following is a description of several of the important directories for Active Workspace customization. Not all directories present in the environment are shown.  
  
  ![image](https://user-images.githubusercontent.com/76819369/130231784-2294346b-6a10-4c09-aa82-f442d74945db.png)

stage
This is the base directory for Active Workspace customization. It is located in TC_ROOT\aws2. This is the root of the development environment. Open this folder with your JavaScript project editor.

repo
This directory contains the declarative source code for Active Workspace, and is required when building the application.

You can use the declarative source definitions in this directory for reference; all of the installed OOTB kits are located here in their respective directories.
out
This is where the local build can be found.

site
This directory is analogous to a WAR file. It is a live application web site which can be served by the gateway, if you configure your gateway to view your local site. Doing this ignores the normal site, which is stored in the file repository.

src
The files and directories located here are for your customizations. They are pre-populated with actual source code and resources that are built along with the contents of the repo directory. The src directory contains the following directories:

image
Contains the icons used by the Active Workspace UI are located here. If you want to add custom icons for your modules, place them in this directory. Follow the file and naming conventions for icons as specified in the UI Pattern Library, located on Support Center.

mysamplemodule
This is an example custom module that you might create. If you use the generateModule script, this is the module that is automatically created if you don't use another one. You may have as few or as many modules as you need to organize your content, but each module must be registered in the main kit.json file, which is located in the solution directory.

Each module will have its own module.json file and must conform to the declarative file and directory structure.

solution
In this directory, you will find the Active Workspace kit.json file and all of the workspace definitions. Your custom modules must be registered in this file for the build script to find and process them. When you use the generateModule script to create your module, it will register your custom module in the kit.json for you.

 Using Action Builder
Use the Actions page of Command Builder or Panel Builder to define their behavior. If you make any changes, select Save Action Flow  to save your changes.

The Actions panel
![image](https://user-images.githubusercontent.com/76819369/130232034-173f4fff-5c33-497d-98d9-85275b737534.png)

Find and select the action you wish to view.

Use the Actions viewer to scroll and zoom around the action flow. Select an action or operator.

Use the Action Properties panel to view the various properties of the selected action or operator.

The Action Palette
![image](https://user-images.githubusercontent.com/76819369/130232060-33bd0e56-52c5-477f-8e18-69a64cfd34f8.png)

Select Toggle Action Palette to display or hide this panel.

Use Operators for splits and events as well as the start and end of the flow.

Use Object Activities to define behavior during the action flow. Drag new activities onto the action flow to create new nodes.

Adding existing actions
You can search for and add existing actions to your action flow.
![image](https://user-images.githubusercontent.com/76819369/130232078-aef76892-839b-4f93-af65-06d101d2ee47.png)


Switch to the Existing tab to search for actions.

Drag an action into the action viewer.

Creating connections
![image](https://user-images.githubusercontent.com/76819369/130232101-0d17b57f-56b4-4e68-86e6-82c6e1dd1855.png)

Toggle the Enable connection setting to create flow lines between actions.

Draw connections between a circle of one action to a circle on another action.

By default, a success connection is drawn. You can change it to a failure connection by selecting the connection, and choosing Failure in the CONNECTION PROPERTIES panel.
![image](https://user-images.githubusercontent.com/76819369/130232124-5e792167-76be-415c-94f7-fabf9db4b134.png)


A Success connection is represented by a solid line, while a Failure connection is dashed.

![image](https://user-images.githubusercontent.com/76819369/130232172-f9f87134-dfb0-4f0e-8314-ac4a22ea88d3.png)

Editing properties
![image](https://user-images.githubusercontent.com/76819369/130232197-565161a0-ea4c-439f-9f43-1dd6f0031187.png)

Use this panel to view or edit properties for the action selected in the action flow. After making changes, select Update to save the definition.

  
  
  Using Panel Builder
Use the Panel Builder canvas to create or modify a panel using drag-and-drop.

Navigating nested panels
The Panel Builder supports nested panels. To navigate nested panels:
  ![image](https://user-images.githubusercontent.com/76819369/130232254-c46e7c0d-0042-4c24-8665-4e0875adf307.png)
  
  The breadcrumb shows you where you are in the nested panel hierarchy. In this example, you are at the top: Awp0ShowCreateObject.

The Views area shows you any subpanels that exists. Selecting one will change to that subpanel.

Subpanels are also shown in the main canvas area, and can be selected to change to that subpanel.
  ![image](https://user-images.githubusercontent.com/76819369/130232303-83db78c9-606c-4b3d-9871-b2cfb82a380c.png)

  

  In this example, the breadcrumb shows that you are viewing the Awp0AddObject subpanel, and that it has a parent.

The Views area shows you that there are no subpanels.

Drag and drop elements
Drag elements onto the canvas to create new panel widgets, layouts, or properties.
  
  ![image](https://user-images.githubusercontent.com/76819369/130232405-d9bf4852-9914-4267-b617-9b74ed5b3da7.png)

Save your changes using the Save Changes  button.

Edit properties
Select a UI element on the canvas to edit its properties in the props panel.
  
![image](https://user-images.githubusercontent.com/76819369/130232477-e988f3c2-9cc3-4a46-bdf5-29a29fc9df88.png)

  Save your changes using the Update button.
