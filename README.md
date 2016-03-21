pdlv2
====

Makes simple [Pure Data (aka pd)](http://msp.ucsd.edu/software.html) patches useable as [LV2 plugins](http://lv2plug.in/) utilizing [libpd](https://github.com/libpd/libpd) and [lv2-c++-tools](http://www.nongnu.org/ll-plugins/hacking.html)

Linux only at the moment.

Requirements
----

Only works on Linux as far as I know

Install these:
* [Pure Data](http://msp.ucsd.edu/software.html) can use package manager
* [libpd](https://github.com/libpd/libpd)
* [lv2-c++-tools](http://www.nongnu.org/ll-plugins/hacking.html) can use package manager
* [ruby](https://www.ruby-lang.org) use package manager or rvm
* [bundler](http://bundler.io/) gem or package manager
  * run: **bundle install** from the top project directory

You'll also need the 

Workflow
----
* create your pd patch, save it as *plugins/\<plugin_name\>/plugin.pd*
  * check out the template patch as a reference
  * specify, using messages:
    * **pluginURI**: *http://uniqueURI/for/your.plugin*
    * **pluginName**: *name of your plugin*
    * **pluginLicense**: *http://rdf-uri/to/your/license/*
      * defaults to 'http://usefulinc.com/doap/licenses/gpl'
  * specify control inputs with **receive** objects
    * format: **receive $0-lv2-control_symbol label:Control-Label range: 0 0.5 1**
    * label cannot contain whitespace at this time
    * range is *min* *default* *max*
  * specify control outputs with **send** objects
    * format: **send $0-lv2-control_symbol label:Control-Label range: 0 0.5 1**
    * label cannot contain whitespace at this time
    * range is *min* *default* *max*
  * specify any audio inputs or outputs you want
    * inputs use **adc~**
      * exapmle: 4 inputs would be *adc~ 1 2 3 4*
    * outputs use **dac~**
    * without arguments, or with *1 2*, they default to Input or Output Left, Right
  * include any abstractions in the same directory
* **make**: to build all the plugins
  * this parses the pd file for all the info it needs to build the plugins
* **make install**: to install into ~/.lv2/
  * you can modify this destination by editing *INSTALL_DIR* in the Makefile

References
----

* Lars Luthman's [LV2 programming for the complete idiot](http://www.nongnu.org/ll-plugins/lv2pftci/)
* [RDF for Ruby](http://blog.datagraph.org/2010/03/rdf-for-ruby)
* [pdLV2-stereo](https://github.com/unknownError/pdLV2-stereo)
* [doap rdf](https://github.com/edumbill/doap/) Documentation of a project

TODO
----

* allow specification of audio input and output names
* allow for block sizes less than 64
* allow whitespace in control labels
* [plugin category](http://www.nongnu.org/ll-plugins/lv2pftci/#More_metadata)
* [port groups](http://www.nongnu.org/ll-plugins/lv2pftci/#Port_groups)
* [midi](http://lv2plug.in/ns/ext/midi#MidiEvent)
