## Main use cases

Support use case -  be able to take a dataset from a support kall and spin up an corresponding environment

Canned environment - preset environment that is available for people to just spin up on demand

## Milestones

* [x] First milestone (canned environment): Allow a user to spin up a Linux environment with a pre-set dataset and revision, on demand 

  * we can probably consider simply having everything within the AMI

  * will we need to do anything to ensure that the MAP license doesn’t expire? how does the MAP license expiry actually work?

* [ ] Second milestone (canned environment): Allow a user to spin up a Linux environment with a pre-set dataset, with it updating the latest version of the major revision, on demand [0.5 weeks]

   * another AMI for GP dataset

   * downgrade dataset in AMIs to 9.60.2

* [ ] Third milestone (canned environment): Also spin up a Windows environment which hooks up with the corresponding Linux environment [2 weeks]

  * install swing clients

  * install KDG

* [ ] Fourth milestone (support): Allow a user to provide their own dataset and spin up a Linux environment on demand [3 weeks]

  * Databases

    * transfer over

    * load them up

  * MAP

    * find the right revision

    * transfer over

    * activate license

  * MES

    * find the right revision

    * transfer over

    * create recentparametervalues based on template + dataset recentparametervalues

      * mainly the DB parameters, most other parameters will be populated during the install process

    *  run installation

* [ ] Fifth milestone (support): Add a corresponding Windows environment [1 week]

  * install the required swing clients

  * install KDG

Git repo of intern project for KiwiCloud: https://nzgit.kiwiplan.co.nz/kiwiplan/kiwicloudinternship

Attached are a couple documents that were provided to the 2020 Interns for their KiwiCloud implementation (though they might not be super useful haha)

A terribly old configurations document:  