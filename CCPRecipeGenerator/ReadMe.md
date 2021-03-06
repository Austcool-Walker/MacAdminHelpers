# Automating the generation of Adobe CC package override files for AutoPkg

## ATTENTION: With the release of CC 2019 Adobe has deprecated CCP. You won't get anything newer than the CC 2018 releases. To download CC 2019 packages you have to login to your Adobe Console ([http://adminconsole.adobe.com](http://adminconsole.adobe.com)).
  
This script helps you customize the build process of Adobe CC packages for your organisation.
It generates an override file for each Adobe product and then builds all packages.

This script is based on the AutoPkg project and the CCP Recipes from "Mosen" [https://github.com/autopkg/adobe-ccp-recipes](https://github.com/autopkg/adobe-ccp-recipes).

This script and its workflow has been tested on macOS Sierra, version 10.12.6 and macOS High Sierra, version 10.13.1.

### Prerequisites

To start on a newly installed (build) machine, install the following packages/tools before using the script:
    
- __Creative Cloud Packager from Adobe__  
Get the CCP installer from the Adobe Admin Console or your responsible Adobe contact at your organisation (or download it from here: [https://www.adobe.com/go/ccp_installer_osx](https://www.adobe.com/go/ccp_installer_osx)

- __Xcode Command Line Tools__  
Make sure the Xcode Command Line Tools are installed.

- __Important__  
There must be no other Adobe CC applications or the Creative Cloud application installed on the machine building packages. Otherwise the build process will fail.

- __AutoPkg__  
This script is using AutoPkg to build the packages, it will install it when not present, if you prefer to install/configure AutoPkg manually, please do at least the following steps:  
Install and configure the AutoPkg environment. [http://autopkg.github.io/autopkg](http://autopkg.github.io/autopkg)  
  - If you want to move some folders to other destinations, please define at least the AutoPkg Cache and Overrides folders:  
    `defaults write com.github.autopkg CACHE_DIR /path/to/cache/dir`  
    `defaults write com.github.autopkg RECIPE_OVERRIDE_DIRS /path/to/override/dir`

- __Free disk space__  
Make sure you have enough free space available on the build machine:  
	-	A full CC package set is about 40 GB per language
	-	The CCP Cache needs additional 20-25 GBs

### Configuration	

- Edit the script __CCPReceiptGenerator.sh__  
    - __Organisation__: The name of your Organisation based on the Adobe Dashboard naming  
    - __SerialNumber__: The serial number provided from Adobe, remove the dashes  
    - __LicenseType__: Is either `enterprise` or `team`  
    - __Identifier__: Set the identifier based on your needs (com.company.XY)  
    - __LanguageShort__: This short string is only used for naming the final packages, should be in the same order as the language array: *(EN DE)*
    - __Language__: Add the languages of the install packages as an array: *(en_US de_DE)*  
    Complete list of supported languages and language codes used in Adobe packages:  

		| Language | Code |   | Language | Code |   | Language | Code |
		| :---: | :---: |:---:| :---: | :---: |:---:| :---: | :---: |
		| Czech | cs_CZ |   | Finnish | fi_FI |   | Dutch | nl_NL |
		| Danish | da_DK |   | French Canadian | fr_CA |   | Polish  | pl_PL |
		| German | de_DE |   | French | fr_FR |   | Portuguese (Brazilian) | pt_BR |
		| English (UAE) | en_AE |   | North African French | fr_MA |   | Russian | ru_RU |
		| English (Intl.) | en_GB |   | Hungarian | hu_HU |   | Swedish | sv_SE |
		| English (Israel) | en_IL |   | Italian | it_IT |   | Turkish | tr_TR |
		| **English (U.S.)** | **en_US** |   | Japanese | ja_JP |   | Ukrainian | uk_UA |
		| Spanish | es_ES |   | Korean | ko_KR |   | Chinese Simplified | zh_CN |
		| Spanish (Mexico) | es_MX |   | Norwegian | nb_NO |   | Chinese Traditional | zh_TW |
		
		_The default language for packages is shown in bold_
	- __adminPrivilegesEnabled__: [ true / __false__ ] : Enable this to allow the CC Desktop application to run with admin rights, to let the end user install/update CC apps.
	- __matchOSLanguage__: [ true / __false__ ] : packages are built based on the active language of the logged in user. As we define the languages later, this is set to false.
	- __rumEnabled__: [ true / __false__ ] : Include RUM in the package or not.
	- __updatesEnabled__: [ true / __false__ ] : Define if the end user should be able to update the app.
	- __appsPanelEnabled__: [ true / __false__ ] : Show the app panel to the end user.



### Have the work done
- Run the Creative Cloud Packager one time manually, log in with your Adobe ID and configure the app as you need it in your organisation.

- Run the generator script `CCPRecipeGenerator.sh`  
The recipes are saved in the AutoPkg overrides folder. At the same time
a file with all recipes is generated and can be used to run all recipes at once.  
After the overrides have successfully been generated, you can start the build process. If you don't need all packages built, then edit 'AutoPKGRunSource.txt' and delete all packages you don't want to build.

- Run autopkg to build all packages based on the generated overrides  
`autopkg run --recipe-list ./AutoPKGRunFile.txt` 

- Or run autopkg manually for a single override:  
`autopkg run "PackageName.pkg"`


### Known issues
- This scripts has the same known limitations as the AutoPkg CCP Recipes do.  
[https://github.com/autopkg/adobe-ccp-recipes](https://github.com/autopkg/adobe-ccp-recipes)
