# Custom Jenkins Master

## Plugin and Goovy Sandbox Management

**Plugins:** Instead of listing plugins to install using the `INSTALL_PLUGINS` environemnt variable, you can list them in the `plugins.txt` file instead.  This allows you to easily manage and version plugins for your Jenkins instance.

**Groovy Sandbox Management**:  Some Pipeline scripts may contain methods that require manual approval by an admin to run.  As the admin approves methods, they get added to a file named `scriptApproval.xml` in the `$JENKINS_HOME` directory.  You can copy this file and version it under the `configuration` directory to have it built into your Jenkins master image.  This will save you the trouble of having to re-approve a pile of methods (which is a realy pain).

## Build a New Jenkins Master

You can create a new Jenkins master image stream with the `jenkins-custom-is.yaml` file under the `ocp` folder, then create a new build (ideally pointing to your own Github repo).  For example:

```
$ oc apply -f ocp/custom-jenkins-is.yaml
$ oc apply -f ocp/enkins-bc.yaml
```

When the build is complete, you should have a new Jenkins master image in your project tracked by the `custom-jenkins` ImageStream.

You can then create a new Jenkins instance (command line or UI), but make sure you change the `project` and `image stream` fields to your project and `custom-jenkins:latest` image stream.

Done!

