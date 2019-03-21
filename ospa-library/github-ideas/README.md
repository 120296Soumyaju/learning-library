![](images/GitHub1.png)

## Library for GitHub OSPA Discussion
### Objectives
* Agree to common method for creating OSPA Hands-On Lab documentation using GitHub.
* Develop standard methodology for OSPA teams
* Determine best mechanism for document creation, edit, and deployment

### Issues :warning:
* Only selected **OSPA GitHub Admin** individuals will be able to modify Oracle GitHub's Learning-Library/ospa-library repository(Ale, Dan, John, so far...)
* OSPA management has decided upon individual folders for different teams/products/labs; to date they are: 
  * adw 
  * appdev 
  * appint 
  * atp 
  * big-data-service * db19c
  * exadata-cloud 
  * migration 
  * nosql 
  * security
 
* GitHub and Git do not support modification (Cloning, Branching, Merging) of individual files and/or folders; so, 'Clones' and 'Branches' are copies of entire Oracle Learning Library
* GitHub repositories (repos) have limitations on size of individual files (100MB) and total size of repository (1GB)
### Contents
* Contents stored on GitHub will be:
  * .md (Markdown) files - These are the main files containing labs instructions
  * .html (HTML5) files - [Optional] If developers want to wrap the content and make it available on a static site
  * misc. SMALL lab files [Optional]
  * larger files will be **LINKED-to** not included in-line [Optional]
* Developers will create and modify content then pass it to "Admins" to update in staging learning-library and ultimately production learning-library
* Developers will be responsible for CE and QA of their own material; peer review will be essential
* Documents will be stored in appropriate folders in learning-library/ospa-library
  * Developers might create entirely new documents
  * Developers might modify existing documents
### Mechanism
* Three-level OSPA repository (repo) scheme
   1. Oracle Learning-Library (production)
   1. OSPA Learning-Library (staging, one of Ale's, Dan's, or John's - tbd)
   1. One 'Developer Repo' for each folder identified earlier
      1. Developers will have full authority to Developer Repos - **Note: Developers Github Access is required**
      1. Developers will create, modify, and review documents in Developer Repos
* We suggest a simple editor for Markdown like the Microsoft Visual Studio Code tool available on [MyDesktop](http://mydesktop.oraclecorp.com/myd/myd_software_licenses.show_complete_list) though any text editor will do
### Alternative Mechanism
* Two-level OSPA repository (repo) scheme
   1. Oracle Learning-Library (production)
   1. OSPA Learning-Library (staging, one of Ale's, Dan's, or John's - tbd
* Developers create .zip file for desired folder and make it available to "Admins" for unzip and load. Zip file will be share out of the band (email, LCMS, Slack) and Developer Github access is not required.
### Suggested Workflow(s)
   1. (If new) Developer checks to see if appropriate folder already in repository; if not, request from "Admins"
   1. Developer creates (or gets from somewhere) desired content, makes sure it is in proper form (.md, .html), and that all large files are linked-to rather than part of document (we need to decide if links will be to Confluence, OraDocs, LCMS, etc...)</br>
   __NOTE:__ We can supply a command to copy a relevant folder to a developer's machine
   1. Developer will push to appropriate "Developer Repo" (e.g. ospa-lib-appdev)
   1. Developer (peers, maybe manager, maybe testers...) review content in GitHub; repeat 2-3-4 cycle until happy
   1. Developer notifies "admin" that "Developer Repo" is ready to go
   1. Admin copies contents from "Developer Repo" into "Staging Repo" (we will script this); performs cursory check of file sizes and formatting
   1. Developer (and team) review document in "Staging Repo" and let Admin know when ok
   1. Admin __MERGEs__ from "Staging Repo" to "Production Repo" - lets Developer know of success/failure
   1. Developer performs final check of "Production Repo"

### Demo
We were asked to create a "live demo" of how this will work; here are the steps we will follow:

1. John will demo [oracle/learning-library/ospa-library](https://github.com/oracle/learning-library) ("Production Repo"); [jjking2019/learning-library/ospa-library](https://github.com/jjking2019/learning-library) ("Staging Repo"), and the "Developer Repos"
1. Dan will create new document for ??? folder and post to ??? repository
1. Dan and peers/manager will review content
1. Dan will let Ale know (email or slack) that changes are ready to go
1. Ale will push to "Staging Repo"
1. Dan and peers/manager will review on "Staging Repo"
1. Dan will let Ale know changes ok
1. Ale will merge changes to "Production Repo"
1. Dan will double-check on "Production Rep"
