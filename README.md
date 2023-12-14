#DocScaler - Tool to generate an installation report for DDN systems

#OSX only
If you don't have brew on MacOSX, you need to execute this first:
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

Install some os dependencies:
brew install xz
brew install pyenv

#All
Install the python dependecies:
pip install -r requirements.txt


#Execution:
./docscaler -c <config file>


#Configuration:
Best practice would be to create a directory and put all relevant files in there.
A configuration template (config.json) can be found in the templates directory.

###GENERAL:
Document related information

	"general": {
			"date": "now",			//Required
			"document_name": "",		//Required
			"title": {			//Optional 
            		"1": "",
            		"2": "",
            		"3": ""
			}
		}
		
date	            -> The document creation date (currently only now is possible)<br>
document_name	> The filename of the document<br>
title			> 3 lines of extra data for the document, e.g. project name<br>


##CUSTOMER:
Customer related information

	"customer": {
			"company": "",			//Required
			"logo": "",			//Required
			"name": "",			//Required
			"phone": "",			//Required
			"email": "",			//Required
			"address": {			//Optional
            		"1": "",
            		"2": "",
            		"3": ""
			}
		}

company 		> The company name
logo			> Image of the company logo. Only the name, if in the same path as the config.
name 			> Name of the customer
phone			> Phone number of the customer
email			> Email address of the customer
address			> Address of the customer site. Can be extended with more lines.


##DDN:
DDN team information

	"ddn": {
			"team": [
				{
					"role": "",
					"name": "",
					"phone": "",
					"email": "",
					"doc_creator": "no"
				}
			]
		}

role			> The role within DDN e.g. Sales Manager
name			> Name of the DDN person
phone			> Phone number of the DDN person
email			> Email address of the DDN person 
doc_creator		> Is this person the creator of the doc? yes/no


##NETWORK:
Network diagrams of the project

	"network": {
			"rack_diagram": "",
			"network_diagram": ""
		}
		
rack_diagram		> Image of the rack diagram. Only the name, if in the same path as the config.
network_diagram		> Image of the network diagram. Only the name, if in the same path as the config.

You can also specify the rotation and the scale for the image like this:
"image.png:<scale>:<rotate>" where scale is in percentage, meaning 50% shrinks the image and the rotation in 
degrees e.g. 90


##FILESYSTEMS:
The filesystem normally consists out of an SFA and Lustre. Here you can specify the FS name and the SFAs
and Lustre Servers that belong to that filesystem. 

	"project": {
		"fs1": { 
			"sfa": { 
				"sfa[1-2]": "<sss_filename>"
			},
			"lustre": {
				"lustre[1-2]": "<esctl_filename>"
			},
		},
		"fs2": { 
			"sfa": [ "<sss_filename>" ],
			"lustre": "<esctl_filename>"
		}
	}
		
sss_filename	> Name of the show sub summary file. Can be a text or tgz file. Only the name, if in the same path as the config.
esctl_filename  > Name of the esctl tar.gz file. Can hold the config of only one node. If you have different configs on different hosts,
                  include them in the esctl

##TEMPLATES:
All templates used for the doc. The order is defined by the number.
Have a look into the template folder for all templates. 
To add your own version to your document, copy the template you would like to change to the manual folder.
It will be automatically taken and "overrides" the original version.

	"templates": {
			"1": "contact",
			"2": "overview",
			"3": "summary",
			"4": "rack_network",
			"5": "project",
			"6": "lustre_snapshot",
			"7": "maintenance",
			"8": "support",
			"9": "appendix"
		}

