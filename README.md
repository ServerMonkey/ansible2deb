ansible2deb(1) -- Create a .deb package from an ansible role or collection
=============================================

## SYNOPSIS

`ansible2deb <ANSIBLE_TYPE> <NAMESPACE> '<MAINTAINER>' [-k]`

## OPTIONS

* `-h`, `--help` :
  Displays the help screen.

* `-k` - Keep version. Will not automatically increase the minor version number
  on each new build"

## DESCRIPTION

ANSIBLE_TYPE defines where to search for the 'role' or 'coll' to be packaged.

NAMESPACE parameter format: 'myusername.rolename' or similar

ANSIBLE_TYPE and NAMESPACE must exist as role- or collection-folder in:  
`~/.ansible/collections/ansible_collections/<NAMESPACE>` or  
`~/.ansible/roles/<NAMESPACE>`  
Create a symlink to your role or collection folder, if it is located somewhere
else.

MAINTAINER parameter format, in quotes: 'Name Lastname <mail@example.com>'

In the base folder of your Ansible role or collection create a file called
'pkg.txt'  
To that file, add variable lines similar to a .deb 'control' file.

### VARIABLES

The following variables are supported:

`Version:` Same as Debian control file
`Depends:` Same as Debian control file, 'ansible' will be added automatically
`Description:` Same as Debian control file
`Ansible-Section:` Marks the package as certain role or collection. Can be
used by other applications to define how the package is used. See below.  
You have to choose what kind of subcategory the package is.

Ansible-Section can be one of the following:

`galaxy-playbooks` - builds as collection  
`galaxy-roles` - builds as collection  
`role` - builds as role  
`role-tasks` - builds as role  
`scripts` - builds as role

Ansible-Section purpose:

`galaxy-playbooks` - for playbooks inside a galaxy collection  
`galaxy-roles` - for roles inside a galaxy collection  
`role` - for a single role, that is not part of a Galaxy collection  
`role-tasks` - for tasks from a single role, that is not part of a Galaxy
collection  
`scripts` - for loose playbooks and scripts that are not part of a role or a
Galaxy collection

The file pkg.txt itself will be packaged as well. Parse the section
'Ansible-Sections' to be used by other applications.

## EXAMPLE

Create the file `~/.ansible/roles/my.cowapp/pkg.txt` with the following:

```
Version: 1.2.3
Ansible-Section: tasks-from-roles
Depends: cowsay (>=3.0), dict
Description: Ansible role to print random text with cowsay
```

Then build the package with:

    $ ansible2deb role my.cowapp 'Peter Miller <peter@example.com>' -k"
