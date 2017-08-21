# Tintorera

TINTORERA SOURCE CODE INTELLIGENCE

https://github.com/vulnex/tintorera
	
(C) 2017 VULNEX http://www.vulnex.com

Table Of Contents
=================

* [Overview](#overview)
* [Install](#install)
* [Toolbox](#toolbox)
* [Usage](#usage)
* [TODO](#TODO)
* [Kudos](#kudos)

---------------------------------------------------------------
# Overview
---------------------------------------------------------------

Source Code Intelligence Framework

---------------------------------------------------------------
# Install
---------------------------------------------------------------

1) Check you GCC version support plugins (GCC 4.6 or later).
2) Install GCC Plugin Dev package that matches your GCC version.
3) Install and build [GCC Python Plugin](https://gcc-python-plugin.readthedocs.io/en/latest/). The recomended version is version 0.15.
4) Copy Tintorera to a folder. Copy `tintorera_lib` folder to  GGC Python Plugin folder
5) Edit analyzer.py and end of file add the path to tinto.json config file

    do_config = tintolib.Read_Config_File("/tintorera/tinto.json")

---------------------------------------------------------------
# Toolbox
---------------------------------------------------------------

* analyzer.py : The magic that runs inside GCC collecting information
* reporter.py : Generates a HTML report from data collected by analyzer.py
* profaniter.py : File agnostic tool to collect profanity words in files
* osinter.py : File agnostic tool to collect OSINT patterns in files 
* multireporter.py : Generates HTML reports for profanity, osinter, etc. 

---------------------------------------------------------------
# Usage
---------------------------------------------------------------

1) Depending how you did install GCC Python Plugin, you must export the python.so library.
  example: `# export LD_LIBRARY_PATH=/path_to/gcc-python-plugin-0.15/gcc-c-api`
2) Configure Tintotera configuration file `tinto.json`
  `output_dir`: Tintotera folder path
  `data_dir`: Tintotera data folder path
3) On the project you want to analyze, edit the Makefile and search for CC or any call to GCC. Add the following line:
  
    CC = gcc -fplugin=/path_to/gcc-python-plugin-0.15/python.so \
    -fplugin-arg-python-script=/path_to/tintorera/analyzer.py

  To compile a simple project / file:
  
    # gcc -fplugin=/path_to/gcc-python-plugin-0.15/python.so \
    -fplugin-arg-python-script=/path_to/tintorera/analyzer.py \
    -o test test.c
   
4) You can run additional tintotera tools to collect more data.
5) Run multirepoter tool if you did run any other tintotera tools.
  example: `# python multirepoter.py -c tinto.json -t 1`
6) Run repoter.py to generate full HTML report
  example: `# python reporter.py -c tinto.json`

---------------------------------------------------------------
# TODO
---------------------------------------------------------------

Whete to start :)
Recomendations? Send us email!

---------------------------------------------------------------
# Kudos
---------------------------------------------------------------

Thanks to:

* GCC Team
* David Malcon for GCC Python Plugin
