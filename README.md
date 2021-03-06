# Check the FH Oberösterreich's Levis automatically for new exam results with Slack notification
##at https://levis.fh-ooe.at

##How does it work?
The Chrome browser is opened and the Levis webpage is called. The login data is inserted and the form submited. On the logged-in grading overview the name of the newest graded course is compared with the one given by you. If it doesn't equal this name there must be a new exam result.

A Slack notification is only sent if there is a new grade online or if the check failed for some reason.

Be aware that the opening of the browser will take the system's focus to this window. Running it not on your primary computer is therefore recommended (or run it in a virtual machine). Tested on Linux and Windows! Should work on OSX too.

##Requirements:
- Chrome browser
- Java
- Node.js with NPM

##Setting up:
install Nightwatch globally:
`npm install -g nightwatch`

then run `npm install` within the root of the project.

In order to get only notifications on new grades unfortunately a file has to be replaced manually (the current version is not in the npm repository):
Replace `node_modules/nightwatch-slack-reporter/lib/reporter.js` with this file:
https://raw.githubusercontent.com/ngs/nightwatch-slack-reporter/master/lib/reporter.js

**personal.json**
- Duplicate `personal.json.template` and rename it to `personal.json` (in `config` folder). 
- Set the FHOÖ login data and the Slack webhook url accordingly.
- Set the path to the chromedriver executable according to your operating system (relative from the project root!)
- Enter the name of your latest graded course in the property `latestCourseGraded`. It's the one at the very top shown in Levis - in the example underneath it would be Augmented Reality.

![Screenshot](/screenshot.png)


##Run it:
`nightwatch`
that way it's run once.

For letting it run every x seconds choose a tool of your choice. 
- On Linux one could use watch:`watch -n600 nightwatch`
- In the Windows PowerShell you could use: `while(1){nightwatch; sleep(600)}`

Those examples run the check every 10 minutes. 
