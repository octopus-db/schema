# octopus-db-schema

## OCTOPUS database schema

This is a visual HTML representation of the OCTOPUS relational database [1].
This repository's content was created using SchemaSpy 6.2.4 (https://schemaspy.org/, https://schemaspy.readthedocs.io/en/v6.2.0/).

If you'd like to learn more about the OCTOPUS project, please visit ...

* OCTOPUS database web interface: https://octopusdata.org
* OCTOPUS database documentation: https://octopus-db.github.io/documentation/
* OCTOPUS database accompanying peer reviewed publication: https://doi.org/10.5194/essd-14-3695-2022

## A way to run SchemSpy on your database

SchemaSpy is a Java-based software that creates database documentation of even highly complex relational database database management systems (DMS).
Here is *one way* to run SchemaSpy (from the terminal on your **Mac**). BTW SchemaSpy will only look at your database's structure, but never at its content. We, therefore, consider it safe to use.

### Open Terminal

Open the Terminal on your Mac. You can find it in the *Applications > Utilities* folder, or you can use *Spotlight search* (Cmd + Space and then type "Terminal").

### Install Homebrew

Homebrew is a command-line package manager for macOS, simplifying both software and libraries installation. Homebrew is highly useful, way beyond the installation of SchemaSpy software.

To install Homebrew, paste the following in your macOS terminal ...

    /bin/bash -c "$(curl -fsSL https//raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"

... then follow the instructions.

### Download and install SchemaSpy

Visit the SchemaSpy GitHub releases page and download the latest release (`.jar` file). Save it to a directory on your machine.

Alternatively just paste ...

    curl -L https://github.com/schemaspy/schemaspy/releases/download/v6.2.4/schemaspy-6.2.4.jar \
    --output ~/Downloads/schemaspy.jar

... to your terminal. You'll find the file in Downloads. Move it to a directory on your machine.

### Download and install Graphviz

SchemaSpy relies on Graphviz for generating graphical representations of the database schema. To install Graphviz paste the following homebrew command in your macOS terminal ...

    brew install graphviz

... and Homebrew will do the job for you.

### Download JDBC driver

A JDBC driver is a software component allowing a Java application, in this case SchemaSpy, to talk to a database. The JCBD driver will have to match your DMS, which is PostgreSQL in the OCTOPUS case. You'll find the latest PostgreSQL via https://jdbc.postgresql.org. However, no matter what DMS, download the matching JDBC driver `.jar` file and save it to the directory where the SchemaSpy `.jar` file is already sitting.

Alternatively  just paste ...

     curl -L https://jdbc.postgresql.org/download/postgresql-42.5.4.jar \
    --output ~/Downloads/jdbc-driver.jar

... to your terminal. You'll find the file in Downloads. Move it to a directory on your machine.

### Run SchemaSpy

Create a `schemaspy.properties` file within that directory, where you set the parameters for SchemaSpy. Here is an example 

    # type of database. Run with -dbhelp for details
    schemaspy.t=pgsql
    # optional path to alternative jdbc drivers.
    schemaspy.dp=./your_JDBC_driver.jar
    # database properties: host, port number, name, user, password
    schemaspy.host=your_database_host
    schemaspy.port=your_port
    schemaspy.db=your_database_name
    schemaspy.u=your_username
    schemaspy.p=your_password
    # output dir to save generated files
    schemaspy.o=./output_directory
    # db schema for which generate diagrams
    # change in case public should be the wrong db schema
    schemaspy.s=public

Replace the placeholders (your_database_host, your_database_name, your_username, your_password, output_directory etc.) with your actual database connection details and desired output directory.

In terminal, use the `cd` command to navigate to the directory where you saved SchemaSpy and the JDBC driver for your database. For example

    cd /path/to/schemaspy-directory

Within the above path, run the following command to run SchemaSpy

    java -jar schemaspy.jar

(in case this causes an cairo error try
    java -jar schemaspy-6.2.4.jar -vizjs
)

### View the Output

Once SchemaSpy completes, open the generated HTML report in your web browser. The main HTML file is usually named `index.html` and is located in the output directory you specified.
Remember to replace placeholder values in the command with your actual database connection details. If you encounter any issues, refer to the SchemaSpy documentation or check for error messages in the terminal for troubleshooting.

----

[1] OCTOPUS (https://octopusdata.org) is an Open Geospatial Consortium (OGC) compliant web-enabled database that allows users to visualise, query, and download cosmogenic 10Be and 26Al, luminescence, and radiocarbon ages and denudation rates associated with erosional landscapes, Quaternary depositional landforms and archaeological records, along with associated geospatial (vector and raster) data layers. OCTOPUS is non-commercial, non-profit, and least restrictively licensed. The main purpose of the database is the sustainment, upcycling and public provisioning of valuable legacy data that would otherwise be lost to the research community. Beyond research, the promotion and implementation of Indigenous self-management, public training and education are declared OCTOPUS focus target scopes.
