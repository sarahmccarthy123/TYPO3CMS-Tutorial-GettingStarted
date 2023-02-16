.. include:: /Includes.rst.txt

.. index:: installation, deployment, requirements

.. _install:

================
Installing TYPO3
================

Welcome to the TYPO3 installation guide. This guide covers each of the steps required
to install TYPO3 using Composer.

For more information on how to deploy TYPO3 to a live environment, visit the :ref:`deploying TYPO3 <DeployTYPO3>` chapter.

Pre-installation Checklist
--------------------------

- Command line (CLI) access with rights to create directories and symbolic links.
- Access to `Composer <https://getcomposer.org>`__ via the CLI (for local development)
- Access to the web server's root directory
- Database with appropriate credentials

Execute Composer Create-Project
-------------------------------

.. tabs::

   .. group-tab:: bash

       .. code-block:: bash

         composer create-project typo3/cms-base-distribution:^11 example-project-directory

   .. group-tab:: powershell

       .. code-block:: powershell

         composer create-project "typo3/cms-base-distribution:^11" example-project-directory

   .. group-tab:: ddev

       .. code-block:: bash

           # Create a directory for your project
           mkdir example-project-directory

           # Go into that directory
           cd example-project-directory

           # Tell DDEV to create a new project of type "typo3"
           # 'docroot' MUST be 'public'
           ddev config  --project-type=typo3 --docroot=public --create-docroot

           # Start the ddev instance
           ddev start

           # Fetch a basic TYPO3 installation composer.json
           ddev composer create "typo3/cms-base-distribution:^11" --no-install -y
           
           # And do the installation
           ddev composer install


This command pulls down the latest release of TYPO3 and places it in the
:file:`example-project-directory`.

After this command has finished running, :file:`example-project-directory`
will have the following structure:

.. code-block:: none

    .
    ├── .gitignore
    ├── composer.json
    ├── composer.lock
    ├── LICENSE
    ├── public
    ├── README.md
    ├── var
    └── vendor


Verify Installation
-------------------

Create an empty file called `FIRST_INSTALL` in the `/public` directory:

.. tabs::

   .. group-tab:: bash

       .. code-block:: bash

         touch example-project-directory/public/FIRST_INSTALL

   .. group-tab:: powershell

       .. code-block:: powershell

         echo $null >> public/FIRST_INSTALL

   .. group-tab:: ddev

       .. code-block:: bash

         ddev exec touch public/FIRST_INSTALL

.. code-block:: none

    .
    ├── .gitignore
    ├── composer.json
    ├── composer.lock
    ├── LICENSE
    ├── public
        ├── FIRST_INSTALL
    ├── README.md
    ├── var
    └── vendor

Access TYPO3 via a web browser
------------------------------

After you have configured your web server to point at the `public` directory in your project
TYPO3 can be accessed via a web browser. The first time a new site is accessed TYPO3 automatically
redirects all requests to :samp:`/typo3/install.php` to complete the installation process.

.. tip::

   When accessing the page via HTTPS you might get a "Privacy error" or similar warning.
   In a local environment it is safe to ignore this warning by forcing the browser to ignore similar
   exceptions for this domain.

   The warning occurs because self-signed certificates are being used.

   If there is a `trustedHostsPattern` error on initial access, try accessing TYPO3 without HTTPS (`http://`).


Scan Environment
----------------

TYPO3 will now scan the host environment. During the scan TYPO3 will check the host system for the following:

- Minimum required version of PHP is installed.
- Required PHP extensions are loaded.
- php.ini is configured.
- TYPO3 has the rights to create and delete files and directories in the installation root directory.

If no issues are detected, the installation process can continue.

If any requirements are not met, TYPO3 will display a list of issues it has detected with suggested solutions.

Once you have made any changes, get TYPO3 to rescan the host environment by reloading the page :samp:`https://example.org/typo3/install.php`.

.. include:: ../Images/AutomaticScreenshots/QuickInstall/Step1SystemEnvironment.rst.txt

Select A Database
-----------------

Select a database connection driver and enter the credentials for the database.

.. include:: ../Images/AutomaticScreenshots/QuickInstall/Step2DatabaseConnection.rst.txt

TYPO3 can either connect to an existing empty database or create a new one.

The list of databases available is dependent on which database drivers are installed on the host.

For example, if you want to use a MySQL database with your TYPO3 instance install the 'pdo_mysql' PHP extension.
Then 'MySQL Database' will be available in the list.(Review)

.. include:: ../Images/AutomaticScreenshots/QuickInstall/Step3ChooseDb.rst.txt

Create Administrative User & Set Site Name
------------------------------------------

An administrator account needs to be created to gain access to TYPO3's backend.

An email address for this user and a site name can be added.

.. include:: ../Images/AutomaticScreenshots/QuickInstall/Step4AdminUserSitename.rst.txt


Initialise
-----------

TYPO3 offers two options for initialisation: creating an empty starting page or
going directly into the backend administrative interface.
Beginners should select the first option and allow TYPO3 to create an empty starting page.
This will also generate a site configuration file.

.. include:: ../Images/AutomaticScreenshots/QuickInstall/Step5LastStep.rst.txt

Next Steps
----------

Now that the installation is complete, TYPO3 can be :ref:`configured <setup>`.

Using DDEV
----------

We also provide a step-by-step tutorial on how to :ref:`Install TYPO3 using DDEV <installation-ddev-tutorial>` 
which includes a video.
