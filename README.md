dans.local-yum-repo
===================

Helper ansible role to create/update a local yum repository to share with a vagrant box for testing.


SYNOPSIS
--------

    ansible-galaxy install [-f] https://github.com/DANS-KNAW/dans.local-yum-repo
    
    
DESCRIPTION
-----------
This ansible role creates and enables a yum repository on the target vagrant box, in a directory that 
is shared with the host machine. The task then copies the RPM packages found in the project's build directory 
to the yum repo and updates the repo's metadata. Now, in subsequent steps the RPM can be installed or 
upgraded on the vagrant box with the `yum` command. 

### Requirements

* The ansible script is run from a directory three levels under the project base directory, such
  as `src/main/ansible`. However, this can be changed by overriding the variable 
  `project_basedir_from_host_machine`.
* The host machine shares the project base directory with the vagrant box, and this directory is  
  mounted at `/vagrant`. This can be overridden by setting the variable `project_basedir_from_vagrant_box`.
* The RPM packages are built using the `rpm-maven-plugin` and are of architecture `noarch`. This can
  be overridden by changing the glob pattern that is used to find the RPMs, in the variable
  `rpms_glob_pattern`.

    