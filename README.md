# vijava-vsphere

**Version: vijava-5.5-beta-vi-v3**

* The `-vi-` suffix indicates that this is an override of original file built by Virtana Inc. with bugfixes.
* The `-v3` suffix indicates that this is the 3rd patch version built by Virtana Inc.
* This repo is a copy of publicy available source code of vijava from https://sourceforge.net/projects/vijava/files/vijava/
* The sourcecode is tested with vSphere 6.5 and 6.7 using `vi-sqe-ui-api` which imports this jar file from Nexus
* There was a bug in the original source code which has been fixed in this repository.
* The output jar of this repo (mvn clean install)

### What's different from original?

**What is different in vijava-5.5-beta-vi-v3 compared to the original vijava-5.5-beta?**

* The original source code was untested with 7.0, it was probably tested only with 6.5/6.7 (and probably explains the beta suffix)
* The vi-sqe-ui-api uses both 6.5/6.7 and 7.0 and since the vmware APIs were changed, this library was failing for 7.0
* The original vijava code was downloaded from sourceforge.net, then the compiled version was reverse engineered using jd-gui (Java Decompiler) and the issues were found and fixed.
* As part of fixing bugs the following jar files were uploaded to vi-nexus.lab.vi.local: `org/doublecloud/ws-util/5.5/ws-util-5.5.jar`
* The source code for org/oublecloud/ws-util-5.5.jar was extracted from an older visphere src jar file and added to the current source repo, so it is always built along with this repo itself. This is just to avoid another repo just for ws-util.
* The original files that were used to debug this vmware code are placed in http://devnull.lab.vi.local/devops/vijava-vsphere-5.5-beta-vi-v3/. 
* They may not be required any more, but kept for reference. 
* This source repo already contains all the required code, so no external references are required.
*  The require libraries like dom4j were either pushed to vi-nexus manually or downloaded via maven-central. 
*  The original `vijava-5.5-beta` project is not maintained by VMWare anymore and original source code is found only in sourceforge.net archives as R297.

### Build

```sh
mvn clean install
```

This will produce `vijava-5.5-beta-vi-v3.jar` which is identical to `viijava-5.5-beta-v3.jar`. The `-vi-` suffix was later added to indicate this was built by Virtana Inc.

### Deployment 

There is no Jenkinsfile attached to this, so the jar file must be manually pushed to vi-nexus. Make sure you update the `<version>vijava-5.5-beta-vi-v3</version>` accordingly.


```sh
# Pushing to vi-nexus
# Ensure you have the settings.xml that has deployment access to vi-nexus
mvn clean deploy -DaltDeploymentRepository=releases::default::http://vi-nexus/content/repositories/releases -s <settings.xml>
```

### SOAP-UI

* The SOAP-UI tool was used to debug the VMWare API. 
* The VMWare API is quite different between 6.5/6.7 and 7.0 which is one of the reasons the original vijava-vsphere had to be fixed for bugs.
* You can download soap-ui from https://www.soapui.org/.
* For any future debugging, the soap-ui xmls are placed in `soap-ui` folder
* Import the `visqeapi-soapui-project.xml` to debug the API.
