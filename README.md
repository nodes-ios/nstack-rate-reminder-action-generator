# nstack-rate-reminder-action-generator

In NStack V2, rate reminders have advanced allowing for clients to define events and assign points to them. Users will then be prompted to rate the app only when specific events have been triggered and points have been accumulated. 
Please see [here](https://nstack-io.github.io/docs/docs/features/rate-reminder.html) for more information on this feature. 

This generator allows you to pass this single build phase tool into your project and on each build, it will generate an enum of all the required actions. It should be used in tandem with the NStack SDK, where you will then be able to pass these event actions to the NStack SDK which will then evaluate annd return whether a rate app alert should be prompted.

A tool to generate rate reminder actions from the [NStack](http://nstack.io) API. 

[![GitHub license](https://img.shields.io/badge/license-MIT-blue.svg)](https://github.com/nodes-ios/nstack-localizations-generator/blob/master/LICENSE)
![Plaform](https://img.shields.io/badge/platform-osx-lightgrey.svg)

## 📦 How to add it to your project
If all you want to do is add this generator to your project to make use of this feature, follow the next steps;

1. First download the latest RateReminderGenerator from the releases [here](https://github.com/nodes-ios/nstack-rate-reminder-action-generator/releases)

2. Create a file in your project named `RateReminderActions.swift`. 
    This will be the file that will be written to with the actions you will need. It should be available in all the targets that require to send these actions to the NStack SDK.
    You can ADD this wherever you would like but I recommend keeping all NStack files close together in a resources directory.
    If you are also using NStack for localizations, I suggest keeping the generated files together like this. 
    <p align="center"><img src="./ReadMeFileManagementSuggestion.png?raw=true" alt="ReadMeFileManagementSuggestion"/></p>
    
3. Place the downloaded generator into where you would like to store it. Note this should be within your project files but it should not be added to any targets within your project. If yuo are using localizations also, I suggest keeping this alongside wherever you haave chosen to keep your `nstack-localizations-generator.bundle`

4. In your Xcode project *(build phases)* add a **New Run Script Phase** and drag it before **Compile Sources** phase
5. Copy/paste in the script below and change your project specific IDs and Paths. 
    If you have worked with NStack-localizations-generator before, this should feel familiar to you. The input is built so you should be able to share the same NStack plist you use for that.
    
    eg;
    ```
    TL_PROJ_ROOT_FOLDER="ProjectName"
    TL_GEN_PATH="${SRCROOT}/${TL_PROJ_ROOT_FOLDER}/Resources/NStack/RateReminderGenerator"
    TL_OUT_PATH="${SRCROOT}/${TL_PROJ_ROOT_FOLDER}/Resources/NStack"
    TL_CONFIG_PATH="${SRCROOT}/${TL_PROJ_ROOT_FOLDER}/Resources/NStack/NStack.plist"

    "${TL_GEN_PATH}" -plist "${TL_CONFIG_PATH}" -output "${TL_OUT_PATH}"
    ```

    To define more; 
    `TL_PROJ_ROOT_FOLDER` should be your projects root folder
    `TL_GEN_PATH` should be the location of the RateReminderGenerator you have downloaded from [here](https://github.com/nodes-ios/nstack-rate-reminder-action-generator/releases) in step one.
    `TL_OUT_PATH` should be the containing directory of where you have added a blank `RateReminderActions.swift` file
    `TL_CONFIG_PATH` should be the NStack plist file. The same one you can use for localizations, containing the Nstack App ID & Rest API Key for your current required NStack app.




6.  Now everytime you do **Clean** and then **Build**, your rate reminder actions will be fetched and models generated and wrote to the file you added in step two.

## 🔧 Working on the script

If you want to work on this script or advance it, you will be able to find the file `RateReminderScript.swift` 
This contains all the code that the gennerator exeecutes so any changes should be made here.

Once you have completed your changes, build the framework and a new generator will be created for you in the root folder of this project. This is done in the build phase of the framework. 

For ease of access to other developers, you should then upload the generator tool to the github releases page along with a tagged release so others can download just the generator without having to download this whole projct.

## 👥 Credits
Made with ❤️ at [Nodes](http://nodesagency.com).

## 📄 License
**nstack-rate-reminder-action-generator** is available under the MIT license. See the [LICENSE](https://github.com/nodes-ios/nstack-localizations-generator/blob/master/LICENSE) file for more info.
