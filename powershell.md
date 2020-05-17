The reality of my work is that I need to work on many different machines with varying configurations. I don't always have the luxury of installing powershell modules, running as administrator, or having the latest version of powershell installed.

The intent is to come up with a list that balances:

* Have commands that are short and memorable.

Some of these commands don't work as-is, and powershell will ask you for the rest of the information. In my opinion this is better than having to type the entire command out with all parameters first go.

* Have commands that work as far back as possible (i.e. powershell version)
* Have commands that don't require special modules to be installed
* My needs

The intent with this is to be as simple as possible.

# Navigation

AutoComplete based on files in current working directory `<TAB>`

# Zip Files
`expand-archive <path to zip file>`
`compress-archive <path to folder>`

# Text Files
Create a blank file
`New-Item -ItemType file example.txt`
`notepad example.txt`

# Miscellaneous

`Get-ComputerInfo`

# Scripts
If the Execution Policy allows execution, simply call the script like a executable file
`.\<script path>`

If powershell scripts are disabled, you can override the permissions by explicitly bypsasing the Execution Policy
`powershell -ExecutionPolicy Bypass -File <script path>`