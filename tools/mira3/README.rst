Galaxy wrapper for the MIRA assembly program (v3.4)
===================================================

This tool is copyright 2011-2013 by Peter Cock, The James Hutton Institute
(formerly SCRI, Scottish Crop Research Institute), UK. All rights reserved.
See the licence text below (MIT licence).

This tool is a short Python script (to collect the MIRA output and move it
to where Galaxy expects the files, and convert MIRA's TCS file into a tab
separated file for use in Galaxy).

It is available from the Galaxy Tool Shed at:
http://toolshed.g2.bx.psu.edu/view/peterjc/mira_assembler 


Automated Installation
======================

This should be straightforward, Galaxy should automatically download and
install the precompiled binary for MIRA v3.4.1.1 for the Galaxy wrapper,
and run any tests.


Manual Installation
===================

There are just two Galaxy files to install:

* ``mira.py`` (the Python script)
* ``mira.xml`` (the Galaxy tool definition)

The suggested location is a new ``tools/mira3`` folder. You will also need to
modify the ``tools_conf.xml`` file to tell Galaxy to offer the tool by adding
the line::
 
  <tool file="mira3/mira.xml" />

If you wish to run the unit tests, also move/copy the ``test-data/`` files
under Galaxy's ``test-data/`` folder. Then::

    $ ./run_tests -id mira_assembler

You will also need to install MIRA, we used version 3.4.1.1. See:

* http://chevreux.org/projects_mira.html
* http://sourceforge.net/projects/mira-assembler/

WARNING: This tool was initially developed to construct viral genome assembly
and mapping pipelines, for which the run time and memory requirements are
negligible. For larger tasks, be aware that MIRA can require vast amounts
of RAM and run-times of over a week are possible. This tool wrapper makes
no attempt to spot and reject such large jobs.


History
=======

======= ======================================================================
Version Changes
------- ----------------------------------------------------------------------
v0.0.1  - Initial version (working prototype, using MIRA 3.2.1)
v0.0.2  - Improve capture of stdout/stderr (should see it as it runs)
v0.0.3  - Support Ion Torrent reads, now requires MIRA 3.4.0 or later
          (some other switches changed, e.g. -OUT rrol to rrot, which
          means the wrapper no longer works with MIRA 3.2.x)
        - The contig summary file (TCS file) was removed in MIRA 3.4
        - Report all missing output files (not just first missing one)
v0.0.4  - Fix problem with backbone arguments inroduced in v0.0.3
v0.0.5  - Implement the <version_command> tag to record the wrapper
          version and the MIRA version being used.
        - Check using MIRA 3.4 (later versions have a different API)
v0.0.6  - Tell MIRA to use /tmp for temporary files
        - Tell MIRA to ignore long read names (otherwise it aborts)
v0.0.7  - Automated installation of the 64 bit Linux MIRA binary.
v0.0.8  - Basic unit test added (but commented out due to Galaxy issue).
        - Link to Tool Shed added to help text and this documentation.
        - Use reStructuredText for this README file.
        - Adopted standard MIT licence.
        - Updated citation information (Cock et al. 2013).
        - Development moved to GitHub, https://github.com/peterjc/pico_galaxy
v0.0.9  - Renamed folder mira_assembler to mira3 (see also MIRA 4 wrapper).
        - Correct path issue in automated dependency installation.
v0.0.10 - Added a functional test.
        - Updated URL for automated installation of MIRA v3.4.1.1
v0.0.11 - Tool definition now embeds citation information.
        - Planemo for Tool Shed upload (``.shed.yml``, internal change only).
        - MIRA 3.4.1.1 dependency now declared via dedicated Tool Shed package.
======= ======================================================================


Developers
==========

This script and related tools were initially developed on the following hg branch:
http://bitbucket.org/peterjc/galaxy-central/src/tools

Development has now moved to a dedicated GitHub repository:
https://github.com/peterjc/pico_galaxy/tree/master/tools/mira_3_4

For pushing a release to the test or main "Galaxy Tool Shed", use the following
Planemo commands (which requires you have set your Tool Shed access details in
``~/.planemo.yml`` and that you have access rights on the Tool Shed)::

    $ planemo shed_update --shed_target testtoolshed --check_diff ~/repositories/pico_galaxy/tools/mira3/
    ...

or::

    $ planemo shed_update --shed_target toolshed --check_diff ~/repositories/pico_galaxy/tools/mira3/
    ...

To just build and check the tar ball, use::

    $ planemo shed_upload --tar_only  ~/repositories/pico_galaxy/tools/mira3/
    ...
    $ tar -tzf shed_upload.tar.gz 
    test-data/empty_file.dat
    test-data/tvc_contigs.fasta
    test-data/tvc_mini.fastq
    tools/mira3/README.rst
    tools/mira3/mira.py
    tools/mira3/mira.xml
    tools/mira3/tool_dependencies.xml


Licence (MIT)
=============

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
