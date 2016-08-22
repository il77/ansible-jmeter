Jmeter role
=========
This ansible role install, configure [Jmeter](http://jmeter.apache.org/) and start distributed tests.

Requirements
------------

This role need Ansible 2.1. It's also supposed that
you are using the merge behaviour for variables (please, see about
[hash_behaviour=merge](http://docs.ansible.com/ansible/intro_configuration.html#hash-behaviour)
for details). Tested on Debian 8

Dependencies
------------

This role doesn't depend from other ansible roles



Role Variables
--------------

Default config variables are described in */jmeter/defaults/main.yml*.
If you need an extended configuration you can specify it in the variables for each environment in section *jmeter.options*. If you want to configure *jmeter.propertise*, *system.propertise* or *reportgeneretor.propertise* you need set parameters in *jmeter.options.name_of_section*.

Example Playbook
----------------

An example of how to use jmeter role:

    - hosts: all
      roles:
        - role: jmeter
          jmeter_version: 3.0
          jmeter:
	  download:
	    jmeter: https://archive.apache.org/dist/jmeter/binaries/apache-jmeter-{{ jmeter_version }}.tgz
	    plugins_manager: https://jmeter-plugins.org/get/
	    cmdrunner: http://search.maven.org/remotecontent?filepath=kg/apc/cmdrunner/2.0/cmdrunner-2.0.jar
	    path: /opt
	    link: /opt/jmeter
	    plugins:
	    options:
	      system:
	      reportgenerator:
	      jmeter:
                - summariser.name=summary
                - beanshell.server.file=../extras/startup.bsh
                - cookies=cookies
                - classfinder.functions.contain=.functions.
                - classfinder.functions.notContain=.gui.
	    testplans:
	      - {test_path: '/opt/tests/weare8_small_mobileapi.jmx', duration: '5', threads: '1', host: 'web01-perf.the8app.com', log_path: '/opt/tests/weare8.jtl', report_path: '/opt/tests/report' }
	    testplans_dependency:
	      - {src: '/opt/tests/feeds.csv', dest: '/opt/tests/'}


License
-------

MIT


Author Information
------------------

Ilya Zaytsev <il77@list.ru>
