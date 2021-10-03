# Create Project 📂

Click `New Project` button in `Operations bar`, a pick box will be popped up

![](../img/op_new_prj_sel.png)

## Pull the template from the Github repository and create the project (recommended)

!> Note: This function requires network connection, please ensure that the network function is ok.

![](../img/quick_start.gif)

1. Open `Operations` bar, click `New Project`, select `From Remote Repository` 

 ![](../img/op_new_prj_sel.png)

 Eide will pull the template information from the default repository, and a dialog box will be popped up asking you to select the template and complete the creation.

 > Tip: You can configure your own template repository location in the plugin Settings. The default repository is the one provided by the author, and you are welcome to share your templates with the default repository via [PR](https://github.com/github0null/eide-resource/pulls)

 ![](../img/op_new_prj_sel_tmp.png)

2. Open the created project and start to configure some of the projects

3. If the template uses the CMSIS package (**if not, you can skip this step**), you need to change the chip type you **want to use**

 ![](../img/prj_sel_dev.png)

 Enable/disable the standard peripherals you want to use by using the **Install/remove peripheral components** in the CMSIS package

 ![](../img/prj_cmsis_component_sel.png)

4. Start Coding.

## Created from eide's built-in project template

> If there is no network and you cannot create from Github templates, Eide also provides some built-in templates, but the numbers are limited.

Open the Operation bar, click on `New Project` and select the `Internal Template` option

![](../img/op_new_prj_sel.png)

Eide will pop up a dialog asking you to select a `project template` and then create a sample project based on the template you have selected.

![](../img/op_new_prj_tmp.png)
