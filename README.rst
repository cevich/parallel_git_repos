Role Name
=========

This role makes it simple to clone from multiple git repositories in parallel.

Requirements
------------

Same as the stock Ansible 2.3 ``git`` module itself.

Role Variables
--------------

``always_force``:
   When true, ignore any/all local modifications for all repositories.  Force
   clone to desired state, destroying whatever might happen to already be there.

``git_op_timeout``:
    Maximum time to wait (in seconds) for each git operation to complete.  Any
    git repo. clone exceeding this will cause the entire role to fail.

``git_op_status_delay``:
    Interval time (in seconds) between each async. status check.  Increase this
    if all/most git repos are relatively large or slow to clone.

``git_def_depth``:
    The default clone depth to use, set this to ``null`` if all/most repos. use
    tag or version references.  Otherwise, simply specify ``depth`` in individual
    ``git_ops``.

``git_ops``:
    List of hashes (dictionaries) which specify Ansible ``git`` module arguments
    and values.  All/most standard arguments are supported.  Both ``dest`` and
    ``repo`` are required, as per usual.

Dependencies
------------

None

Example Playbook
----------------

::

    - hosts: all
      vars:
        git_ops:
           - repo: "https://github.com/ansible/galaxy"
             dest: "{{ playbook_dir }}/path/to/dir/galaxy"
           - repo: "https://github.com/ansible/ansible"
             dest: "{{ playbook_dir }}/path/to/dir/ansible"
           - repo: "https://github.com/ansible/ansible-container"
             dest: "{{ playbook_dir }}/path/to/dir/container"
      roles:
         - cevich.parallel_git_repos

License
-------

    parallel_git_repos makes it simple to clone from multiple git repositories in parallel.
    Copyright (C) 2017  Christopher. C Evich

    This program is free software: you can redistribute it and/or modify
    it under the terms of the GNU General Public License as published by
    the Free Software Foundation, either version 3 of the License, or
    (at your option) any later version.

    This program is distributed in the hope that it will be useful,
    but WITHOUT ANY WARRANTY; without even the implied warranty of
    MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
    GNU General Public License for more details.

    You should have received a copy of the GNU General Public License
    along with this program.  If not, see <https://www.gnu.org/licenses/>.


Author Information
------------------

Causing trouble and inciting mayhem with Linux since Windows 98


Continuous Integration
-----------------------

Travis: |ci_status| image:: https://travis-ci.org/cevich/parallel_git_repos.svg?branch=master
                    :target: https://travis-ci.org/cevich/parallel_git_repos
