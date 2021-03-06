---
title: Creating Rhino Commands Using Python
description: This guide demonstrates how to create Rhino commands from Python scripts.
author: pascal@mcneel.com
apis: ['RhinoPython']
languages: ['Python']
platforms: ['Windows', 'Mac']
categories: ['Getting Started']
origin: http://wiki.mcneel.com/developer/python/commands
order: 1
keywords: ['python', 'commands']
layout: toc-guide-page
---

# {{ page.title }}

{{ page.description }}

## Overview

It is possible, if a little convoluted, to create "real" Rhino commands from Python scripts.  Below is outlined the procedure on Rhino for Windows, with a couple of comments about where the files need to go for this all to work with Rhino for Mac.  The initial template for the commands, along with a new GUID and the appropriate folders are created automatically by the Python script editor on Windows.  So far it is possible but not obvious or automatic to create all this on Rhino for Mac.  It is possible to install the folders and scripts for an existing Python command on the Mac and have it all work.

First, we will cover [Rhino for Windows](#windows), then turn our attention to [Rhino for Mac](#mac).

## Windows

1. Start in the *Rhino Python editor* using the `EditPythonScript` command.
1. Click on the *New* icon, and choose *Command* in the ensuing dialog.
![New Command]({{ site.baseurl }}/images/creating_rhino_commands_using_python_01.png)
1. Enter the command name and the plugin name that you would like to have the command used in - the plugin can be a new one or an existing one.  You can add multiple commands to a plugin.  In this example, we used `MyNewCommand` in *MyNewPlugIn*.  A new script file is generated with the framework for the new command...
![New Script]({{ site.baseurl }}/images/creating_rhino_commands_using_python_02.png)
1. Note that, with Rhino for Windows, the script is automatically saved in a special location:
![Special Script Location]({{ site.baseurl }}/images/creating_rhino_commands_using_python_03.png)
1. The code that the command calls is in the `def RunCommand( is_interactive ):` function.
1. Add your script code here - the template provides some dummy code and a couple of comments, all to be called from this part of the script.  The whole script can be in this one function or you can add other functions as you normally would, as needed.  Make sure to modify the initial `import` statements to suit the script you are writing - the automatic template `imports` are there for the example script provided.
1. Add this line at the bottom of the script `RunCommand(True)`.  This allows you to test the script from the editor, debug etc.  Just remember to comment that line before you distribute the script or try to use it as a command.  It is also possible to write a more "normal" script, test, etc. as needed in the usual way, then just copy and paste into this formatted command script template.
1. In order for this to run as a command in Rhino, the script location needs to be exactly right so that Rhino knows where to look.  On Windows, the path for a command script looks like this: *C:\\Users\\USERNAME\\AppData\\Roaming\\McNeel\\Rhinoceros\\5.0\\Plug-ins\\PythonPlugIns\\MyNewPlugIn \{146e099d-760d-4a6c-8662-96119f3fd62f\}* ...and it must keep that crazy name with the GUID in brackets, and the path that the editor set up when you created the command initially.
![Special Script Path]({{ site.baseurl }}/images/creating_rhino_commands_using_python_04.png)
1. To distribute the script as a plugin, zip the entire folder, in this case making: *MyNewPlugIn \{146e099d-760d-4a6c-8662-96119f3fd62f\}.zip*.
1. *NOTE*: Users will need to unzip to the plugins folder listed above, with Rhino closed.

### Creating an RHI Installer

In the *dev* sub-folder that is created in the plugin folder, create a *py* file named *plugin.py* that has only these lines:

```py
id="{146e099d-760d-4a6c-8662-96119f3fd62f}"
version="1.0.0.1"
title="MyNewCommand"
```

In the above *plugin.py*, the lines mean the following:

- Line 1 has the UUID from the plugin, found in the folder name.
- Line 2 has the version - it would be up to you to keep that current.
- Line 3 has the command name.

With this file in place in the *dev* sub-folder, then you can zip the containing plugin folder (*MyNewPlugIn{146e099d etc etc}*) and then rename it from *.zip* to the *.rhi* extension.  Double-clicking this *rhi* file on another system (Rhino closed) should install all the files in the correct location for that user.  Rhino should then see the command as a regular command.

*NOTE*: sometimes, using this system, Rhino requires that Python be loaded before it can see the command the first time in a session - running `EditPythonScript`, or any other script should allow the command to work.

## Mac

Setting this up on Mac OS X is a bit more labour intensive, but once you see how it works, it should be fairly straightforward. (It is helpful to read the [Windows](#windows) section above to get the general idea).  

There are four things you need to pay attention to on OS X:

1. The py script file
1. The plugin name
1. The command name
1. The plugin GUID

On OS X, the location of the plugin folders must be in:

*/Users/~/Library/Application Support/McNeel/Rhinoceros/MacPlugIns/PythonPlugIns/*

If the *PythonPlugIns* folder does not yet exist, you'll have to create it.

Within that folder there needs to be a folder for each command plugin such as

*PythonPlugIns/MyNewPlugIn {146e099d-760d-4a6c-8662-96119f3fd62f}*

and within the individual plugin's folder there is yet another folder called *dev* - that is where the Python script itself should be saved.  The script name must have a special format as well - again, not automatic on Rhino for Mac, so you'll need to be careful to get it right.  The file name must be in the format:

*CommandName_cmd.py*

There can be multiple command files in the folder - one for each command in the plugin.

The long messy number thing in braces is the GUID - that GUID, and in fact the folder itself, is automatically generated on Rhino for Windows when you tell the editor you want to create a command - but on OS X you need to create the GUID and the folder and *dev* sub-folder yourself.  [Generate a GUID](https://www.guidgenerator.com/online-guid-generator.aspx) and then use it in the folder name as indicated above: *PlugInName{GUID}*

The Python script itself has to be set up and named correctly as well - this is done from a template on Rhino for Windows, buy you will need to do it by hand, so to speak, on OS X.  The *py* file should be set up like this:

```py
#import statements as needed:
import rhinoscriptsyntax as rs
import scriptcontext as sc
import Rhino
#this line with the name of the command:
__commandname__ = "MyNewCommand"
def RunCommand( is_interactive ):
     #Your code in here
     obj = rs.GetObject()
     if obj:
         print "Got an object"
     #etc...
```

This command script must be saved to:

*/Users/~/Library/Application Support/McNeel/Rhinoceros/MacPlugIns/PythonPlugIns/PlugInName{GUID}/dev*

*NOTE*: the command name must match the script file file name, so in this example the file name would be: *MyNewCommand_cmd.py*
