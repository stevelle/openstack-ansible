OpenStack Ansible Deployment
############################
:tags: openstack, cloud, ansible
:category: \*nix

contributor guidelines
^^^^^^^^^^^^^^^^^^^^^^

Bugs
----

Bugs should be filed on Launchpad at "https://bugs.launchpad.net/openstack-ansible".

When submitting a bug, or working on a bug, please ensure the following criteria are met:
  * The description clearly states or describes the original problem or root cause of the problem.
  * Include historical information on how the problem was identified.
  * Any relevant logs are included.
  * If the issue is a bug that needs fixing in a branch other than master, please note the associated branch within the launchpad issue.
  * The provided information should be totally self-contained. External access to web services/sites should not be needed.
  * Steps to reproduce the problem if possible.

Tags:
    If it's a bug that needs fixing in a branch in addition to master, add a '\<release\>-backport-potential' tag (e.g. ``juno-backport-potential``).  There are predefined tags that will auto-complete.

Status:
    Please leave the **status** of an issue alone until someone confirms it or a member of the bugs team triages it. While waiting for the issue to be confirmed or triaged the status should remain as **New**.

Importance:
    Should only be touched if it is a Blocker/Gating issue. If it is, please set to **High**, and only use **Critical** if you have found a bug that can take down whole infrastructures. Once the importance has been changed the status should be changed to *Triaged* by someone other than the bug creator.

Triaging bugs:
    Reported bugs need prioritization, confirmation, and shouldn't go stale. If you care about OpenStack stability but aren't wanting to actively develop the roles and playbooks used within the "os-ansible-deployment" project consider contributing in the area of bug triage, which helps immensely. The whole process is described in the upstream `Bug Triage Documentation`_.


Submitting Code
---------------

* Changes to the project should be submitted for review via the Gerrit tool, following the `workflow documented here`_.
* Pull requests submitted through GitHub will be ignored and closed without regard.
* All feature additions/deletions should be accompanied by a blueprint/spec. IE: adding additional active agents to neutron, developing a new service role, etc...
* Before creating blueprint/spec an associated issue should be raised on launchpad. This issue will be triaged and a determination will be made on how large the change is and whether or not the change warrants a blueprint/spec. Both features and bug fixes may require the creation of a blueprint/spec. This requirement will be voted on by core reviewers and will be based on the size and impact of the change.
* All blueprints/specs should be voted on and approved by core reviewers before any associated code will be merged. For more information on blueprints/specs please review the `upstream OpenStack Blueprint documentation`_. At the time  the blueprint/spec is voted on a determination will be made whether or not the work will be backported to any of the "released" branches.
* Patches should be focused on solving one problem at a time. If the review is overly complex or generally large the initial commit will receive a "**-2**" and the contributor will be asked to split the patch up across multiple reviews. In the case of complex feature additions the design and implementation of the feature should be done in such a way that it can be submitted in multiple patches using dependencies. Using dependent changes should always aim to result in a working build throughout the dependency chain. More information on `advanced gerrit usage and dependent changes can be found here`_.
* All patch sets should adhere to the Ansible Style Guide listed here as well as adhere to the Ansible best practices when possible. `Ansible best practices can be found here`_.
* All changes should be clearly listed in the commit message, with an associated bug id/blueprint along with any extra information where applicable.
* When cherry-picking a commit from one branch to another the commit message should be amended with any files that may have been in conflict while performing the cherry-pick operation. Additionally, cherry-pick commit messages should contain the original commit *SHA* at the bottom of the new commit message. This can be done with ``cherry-pick -x``. Here's more information on `Submitting a change to a branch for review`_.
* Refactoring work will never be backported to a "released" branch. Additionally, refactoring work should never include additional "rider" features. Features that may pertain to something that was re-factored should be raised as an issue and submitted in subsequent patches.


Style Guide
-----------

When creating tasks and other roles for use in Ansible please create then using the YAML dictionary format.

Example YAML dictionary format:
    .. code-block:: yaml

        - name: The name of the tasks
          module_name:
            thing1: "some-stuff"
            thing2: "some-other-stuff"
          tags:
            - some-tag
            - some-other-tag


Example what **NOT** to do:
    .. code-block:: yaml

        - name: The name of the tasks
          module_name: thing1="some-stuff" thing2="some-other-stuff"
          tags: some-tag

    .. code-block:: yaml

        - name: The name of the tasks
          module_name: >
            thing1="some-stuff"
            thing2="some-other-stuff"
          tags: some-tag


Usage of the ">" and "|" operators should be limited to Ansible conditionals and command modules such as the Ansible ``shell`` or ``command``.


.. _workflow documented here: http://docs.openstack.org/infra/manual/developers.html#development-workflow
.. _upstream OpenStack Blueprint documentation: https://wiki.openstack.org/wiki/Blueprints
.. _advanced gerrit usage and dependent changes can be found here: http://www.mediawiki.org/wiki/Gerrit/Advanced_usage
.. _Ansible best practices can be found here: http://docs.ansible.com/playbooks_best_practices.html
.. _Submitting a change to a branch for review: http://www.mediawiki.org/wiki/Gerrit/Advanced_usage#Submitting_a_change_to_a_branch_for_review_.28.22backporting.22.29
.. _Bug Triage Documentation: https://wiki.openstack.org/wiki/BugTriage
