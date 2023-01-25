# ansible2deb
Create a .deb package from an ansible role or collection.

Tested on Debian 11

### How to use
`ansible2deb -h`  

To add additional APT dependencies to your ansible role, create a file named 'ansible2deb.txt' in the base folder of your role or collection.  
In that file add the same line, as you would att to a .deb control file.  
For example this line:  
`Depends: cowsay (>=3.03)`