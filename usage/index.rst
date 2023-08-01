.. _using-bede:

Using Bede
==========

Bede is running Red Hat Enterprise Linux 8 and access to its
computational resources is mediated by the Slurm batch scheduler.

Registering
-----------

Access to the machine is based around projects:

-  For information on how to register a new project, please see `the N8CIR website <https://n8cir.org.uk/supporting-research/facilities/bede/docs/bede_registrations/>`__.

-  To create an account to use the system:

   -  Identify an existing project, or register a new one.
   -  Create an EPCC SAFE account and login to the SAFE system at `safe.epcc.ed.ac.uk <https://safe.epcc.ed.ac.uk>`__
   -  Once there, select "Project->Request access" from the web
      interface and then register against your project

Login
-----

Bede offers SSH and X2GO services running on host ``bede.dur.ac.uk`` (which
fronts the two login nodes, ``login1.bede.dur.ac.uk`` and
``login2.bede.dur.ac.uk``). SSH or X2GO should be used for all interaction with
the machine (including shell access, file transfer and graphics).

.. warning::

   Please use an SSH client and **not** X2GO the first time you ever log in to
   Bede, or immediately after a password reset. Your MFA token will be
   generated, but X2GO will not show it to you.

The login nodes are shared between all users of the service and
therefore should only be used for light interactive work, for example:
downloading and compiling software, editing files, preparing jobs and
examining job output. Short test runs using their CPUs and GPUs are also
acceptable.

Most of the computational power of the system is accessed through the
batch scheduler, and so demanding applications should be submitted to it
(see "Running Jobs").


.. _usage-mfa:

Multi Factor Authentication
---------------------------

When connecting to the login nodes, the system has to validate your
identity. In order to help keep accounts secure, Bede employs a
technique called Multi Factor Authentication (MFA), where something you
know (your password), is combined with something you have (an app on
a mobile device, such as your phone).

When you first login to Bede, or after a password reset, you should use SSH to connect to the machine (rather than x2go) and you will be prompted
to:

1. Change your password
2. Import an MFA token into an app on your mobile device

Instead of `Password`, to login after this you will be prompted for:

- ``First Factor`` - this is your password
- ``Second Factor`` - this is a one-time password code provided by the token in your app

Mobile apps that can be used to import an MFA token include Microsoft Authenticator,
Google Authenticator, and other TOTP authentication clients. When the token is generated on Bede, it will
display a QR code, which can then be imported into the app (e.g. select ``+`` to add
an account and then *Scan a QR code* or *Other account* to scan the QR code).

Please be aware that this MFA token is only for Bede. You may also need
separate tokens to access SAFE and other services, such as those provided by
your home institution. Bede's token should be compatible with any MFA app you
may already be using.

If you are unable to use MFA, for example because of accessibility reasons,
please contact `support <../faq/#faq-helpsupport>`__ for options.

**If you have lost your password or MFA token, please use EPCC's SAFE system to request a password reset for your Bede login account, which we normally aim to process within a working day.**

If you are finding that you are having to use your password and a MFA token too many times, we have provided some tips on `how to reduce the frequency that MFA is required <../faq/#faq-reducemfa>`__.

.. _usage-x2go:

X2GO
----

Running graphical applications over the Internet using an ordinary SSH client
can be quite slow. If you need to run such programs on Bede, you may wish to
consider X2GO as an alternative.

Instructions for installing the X2GO client on Windows, Mac and Linux are on the `X2GO website <https://wiki.x2go.org/doku.php/doc:installation:x2goclient>`__.

.. warning::

   Please use an SSH client and **not** X2GO the first time you ever log in to
   Bede, or immediately after a password reset. Your MFA token will be
   generated, but X2GO will not show it to you.

Once you have installed and launched the X2GO client, provide Bede's connection details by clicking on the *Session -> New session...* menu item to open the *Session preferences - New session* window (this may happen automatically when you first run X2GO). Enter the following details:

* Session name: ``bede.dur.ac.uk``
* Host: ``bede.dur.ac.uk``
* Login: *your Bede username*
* Session type: *select Published applications from the drop down menu*

When you are ready to login, click on the *bede.dur.ac.uk* name in the session selection window, enter your username and click Ok. You will be prompted for your password (or ``First Factor`` and ``Second Factor`` if MFA is enabled) similar to a SSH login.

X2GO should now connect to Bede and show some details such as the *Session Id*. Once you see this, please pay attention to the row of four pale blue icons inside the grey box. These icons are:

* Circular icon - *open published applications window*
* Folder icon - *configure exporting a local directory to Bede*
* Pause icon - *disconnect from your X2GO session, leaving programs running, allowing you to reconnect to it later. If you use this feature, you will need to make sure that all your sessions use the same login node. To do this, follow the instructions above to create an X2GO session, but instead of using the address bede.dur.ac.uk, give the address of one of the login nodes explicitly (either login1.bede.dur.ac.uk or login2.bede.dur.ac.uk*)
* Terminate icon - *close your X2GO session, stopping all running programs*

At this point, Click on the circular icon to open the *Published Applications* window, select *System -> MATE Terminal* and click Start. If there are no applications to select please close the *Published Applications* window, wait for 5 seconds, then open click on the circular icon again.

A terminal window should open, giving you command line access to Bede. Use it to interact with the service and launch applications, including graphical ones, in the usual way.


.. _usage-acknowledging-bede:

Acknowledging Bede
------------------

All work that makes use of the Bede should properly acknowledge the facility
wherever the work is presented.

We provide the following acknowledgement text, and strongly encourage its use:

.. include:: /common/acknowledging-bede.rst

Acknowledgement of Bede provides data that can be used to assess the facility's
success and influences future funding decisions, so please ensure that you are
acknowledging where appropriate.

.. _usage-file-storage:

File Storage
------------

Each project has access to the following shared storage:

-  Project home directory (``/projects/<project>``)

   -  Intended for project files to be backed up
   -  Modest performance
   -  A default quota of ``20GB``

-  Project Lustre directory (``/nobackup/projects/<project>``)

   -  Intended for bulk project files not requiring backup
   -  Fast performance
   -  No quota limitations

By default, files created within a project area are readable and
writable by all other members of that project.

In addition, each user has:

-  Home directory (``/users/<user>``)

   -  Intended for per-user configuration files to be backed up
   -  Modest performance
   -  A default quota of ``20GB``

Please note that, as access to Bede is driven by project use, no
personal data should be stored on the system.

Current utilisation and limits of a user’s home directory can be found
by running the ``quota`` command. Similar information can be found for the
project home directory using the ``df -h /projects/<project>`` command.

To examine how much space is occupied by a project's Lustre directory,
a command of the form ``du -csh /nobackup/projects/<project>`` is
required. As ``du`` will check each and every file under the specified
directory, this may take a long time to complete. We plan to develop
the service and provide this information in a more responsive format in
the future.


Running Jobs
------------

Access beyond the two login node systems should only be done through the
Slurm batch scheduler, by packaging your work into units called jobs.

A job consists of a shell script, called a job submission script,
containing the commands that the job will run in sequence. In addition,
some specially formatted comment lines are added to the file, describing
how much time and resources the job needs.

Resources are requested in terms of the type of node, the number of GPUs
per node (for each GPU requested, the job receives 25% of the node’s
CPUs and RAM) and the number of nodes required.

There are a number of example job submission scripts below.

Requesting resources
~~~~~~~~~~~~~~~~~~~~

Part of, or an entire node
^^^^^^^^^^^^^^^^^^^^^^^^^^

Example job script for programs written to take advantage of a GPU or
multiple GPUs on a single computer:

.. code-block:: bash

   #!/bin/bash

   # Generic options:

   #SBATCH --account=<project>  # Run job under project <project>
   #SBATCH --time=1:0:0         # Run for a max of 1 hour

   # Node resources:
   # (choose between 1-4 gpus per node)

   #SBATCH --partition=gpu    # Choose either "gpu" or "infer" node type
   #SBATCH --nodes=1          # Resources from a single node
   #SBATCH --gres=gpu:1       # One GPU per node (plus 25% of node CPU and RAM per GPU)

   # Run commands:

   nvidia-smi  # Display available gpu resources

   # Place other commands here

   echo "end of job"

Multiple nodes (MPI)
^^^^^^^^^^^^^^^^^^^^

Example job script for programs using MPI to take advantage of multiple
CPUs/GPUs across one or more machines:

.. code-block:: bash

   #!/bin/bash

   # Generic options:

   #SBATCH --account=<project>  # Run job under project <project>
   #SBATCH --time=1:0:0         # Run for a max of 1 hour

   # Node resources:

   #SBATCH --partition=gpu    # Choose either "gpu" or "infer" node type
   #SBATCH --nodes=2          # Resources from a two nodes
   #SBATCH --gres=gpu:4       # Four GPUs per node (plus 100% of node CPU and RAM per node)

   # Run commands:

   bede-mpirun --bede-par 1ppc <mpi_program>

   echo "end of job"

The ``bede-mpirun`` command takes both ordinary ``mpirun`` arguments and
the special ``--bede-par <distrib>`` option, allowing control over how
MPI jobs launch, e.g. one MPI rank per CPU core or GPU.

The formal specification of the option is:
``--bede-par <rank_distrib>[:<thread_distrib>]`` and it defaults to
``1ppc:1tpt``

Where ``<rank_distrib>`` can take ``1ppn`` (one process per node),
``1ppg`` (one process per GPU), ``1ppc`` (one process per CPU core) or
``1ppt`` (one process per CPU thread).

And ``<thread_distrib>`` can take ``1tpc`` (set ``OMP_NUM_THREADS`` to
the number of cores available to each process), ``1tpt`` (set
``OMP_NUM_THREADS`` to the number of hardware threads available to each
process) or ``none`` (set ``OMP_NUM_THREADS=1``)

Examples:

.. code-block:: bash

   # - One MPI rank per node:
   bede-mpirun --bede-par 1ppn <mpirun_options> <program>

   # - One MPI rank per gpu:
   bede-mpirun --bede-par 1ppg <mpirun_options> <program>

   # - One MPI rank per core:
   bede-mpirun --bede-par 1ppc <mpirun_options> <program>

   # - One MPI rank per hwthread:
   bede-mpirun --bede-par 1ppt <mpirun_options> <program>

Multiple nodes (IBM PowerAI DDL)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. warning::

   IBM PowerAI DDL is only supported on RHEL 7.

IBM PowerAI DDL (Distributed Deep Learning) is a method of using the
GPUs in more than one node to perform calculations. Example job script:

.. code-block:: bash

   #!/bin/bash

   # Generic options:

   #SBATCH --account=<project>  # Run job under project <project>
   #SBATCH --time=1:0:0         # Run for a max of 1 hour

   # Node resources:

   #SBATCH --partition=gpu    # Choose either "gpu" or "infer" node type
   #SBATCH --nodes=2          # Resources from a two nodes
   #SBATCH --gres=gpu:4       # Four GPUs per node (plus 100% of node CPU and RAM per node)

   # Run commands:

   # (assume IBM Watson Machine Learning Community Edition is installed
   # in conda environment "wmlce")

   conda activate wmlce

   bede-ddlrun python $CONDA_PREFIX/ddl-tensorflow/examples/keras/mnist-tf-keras-adv.py

   echo "end of job"

.. _usage-maximum-job-runtime:

Maximum Job Runtime
~~~~~~~~~~~~~~~~~~~

Partitions on Bede have default job times, and maximum job times that can be
requested:

.. list-table:: 
  :widths: 1 1 1
  :header-rows: 1

  * - Partition Name
    - Default Job Time
    - Maximum Job Time
  * - ``infer``
    - ``01:00:00``
    - ``2-00:00:00``
  * - ``gpu``
    - ``01:00:00``
    - ``2-00:00:00``

Where, for example, ``2-00:00:00`` means 'two days, zero hours, zero minutes,
and zero seconds'. These job time limits affect what will and won't be accepted
in the ``--time`` field of your job script: ``--time`` values above the partition
maximum will result in your job submission being rejected.

Job Allocation Limits
~~~~~~~~~~~~~~~~~~~~~

There are currently no limits on the total or concurrent number of running jobs per project or per user.
There are also no software-defined limits on the size of jobs (memory, cores, nodes), but jobs must be able to run on the available hardware.

Jobs are scheduled subject to Slurm's `Multifactor Priority Plugin <https://slurm.schedmd.com/priority_multifactor.html>`__, which considers factors such as age, job size and fair-use when selecting jobs for execution.
 