Overview
========

> Git is distributed revision control system with an emphasis on speed, data integrity, and support for distributed, non-linear workflows.

Now, this is great and all, but what it means? Here are some points some people have problem getting about git:

* everything related to git repository is stored in `.git` folder in root of your project; you can just copy project folder and git repository will travel with it
* from technical standpoint, there is no central repository, all repositories are equal
* usually there is one `upstream`, but which repository it is depends on agreement between project members
* this has some (maybe) unexpected side effects
	* you cannot restrict read access to specific files, folders, branches; if you want someone to clone from you, he has to be able to get everything
	* everyone has complete history of the project

All repositories are equal
--------------------------

* while you do clone from somewhere, you are not restricted to pushing/pulling from there
* you have a colleague who made some useful class but it's not ready to be pushed upstream yet? Don't worry, you can pull it directly from him

Restricting access
------------------

* you cannot restrict **read** access to files, directories or branches
	* this can sometimes be problem in corporate environment for direct migration from SVN/TFS to git
* it **is** possible to restrict **write** access
	* git has ability to be extended by hooks, so you can restrict write and/or check other stuff
		* for example, you can verify that commit contains WIT number and reject it otherwise

Everyone has complete history
-----------------------------

* this is very important point
* I'm sure it happened to you at least once, you commit password into source control
	* if someone already cloned/pulled from you, all you can do is change it
	* committing new version without the password won't help you, because everyone has complete history, each and every commit, in the local repository
* other cause where you have to remember this is if you commit some huge file (`.pdb` or something) and later down the line you notice  that your repository is huge
	* deleting the file and committing the deletion won't help (unless you rewrite history and remove the file completely from all commits, see below)
	* the file is part of the repository forever
* **history can be rewritten**, but you will break every repository that cloned from you and they will have to re-clone, losing every local branch
	* in other words, **don't ever rewrite history unless you know what you are doing**