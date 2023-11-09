# Terminal Guide
Author: Prof. Dr. Fc. Gunar Stevens

Co-Author: Barack-O-Llama

## NAVIGATING THE TERMINAL

_ls_ | show files/subdirectories in current directory

	ls    # show visible files/subdirectories
	ls -a     # show all files/subdirectories

_cd_ | change directory

	cd    # go to root directory
	cd ..    # go to parent directory
	cd [directory]

## EDITING/VIEWING FILES

_cat_ | print and edit file

 	# PRINTING FILES
	cat [file]    # print file in terminal
 	cat [file-1] [file-2] [...]    # print concatenated files in terminal

 	# CREATING / OVERWRITING FILES (>)
	cat > [file]    # (over)write text in file (Ctrl-D to exit)
 	cat [file] > [file-redirect]    # copy file to file-redirect
  	cat [file-1] [file-2] [...] > [file-redirect]    # print concatenated files in file-redirect

   	# APPENDING TO FILES (>>)
	cat >> [file]    # add input text to file (Ctrl-D to exit)
	cat [file] >> [file-redirect]    # add file to file-redirect
	cat [file-1] [file-2] [...] >> [file-redirect]    # add concatenated files to file-redirect

   	# NOTE: The file listed after the output redirection symbol (>) will be overwritten, if it already exists.

_less_ | print (long) file

	less [file]

_nano_ | edit file

	nano [file]

_feh_ | view image

	feh [file]

_python_ | run python file

	python [file.py]

_jupyter lab_ | open jupyter lab locally

	jupyter lab
 	jupyter lab [file.ipynb]

## GIT COMMANDS

_git clone_ | create copy of repository on your system

	git clone https://github.com/[user]/[repository].git

_git pull origin_ | update repository on your system

	git pull origin [branch]
