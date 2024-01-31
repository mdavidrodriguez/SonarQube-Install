# SonarQube Installation

Installation of SonarQube in Docker using the Docker Compose plugin.

<a href="https://github.com/EARodriguezM/SonarQube-Install/blob/main/README_es.md"><img src="https://img.shields.io/static/v1?label=&labelColor=505050&message=Spanish README &color=%230076D6&style=flat&logo=google-chrome&logoColor=green" alt="website"/></a>

## Repository Description

The repository has the following structure:
``` bash
├── scripts
│   ├── install-sonar-scanner.sh
├── docker-compose.yml
├── README.md
├── README_es.md
```
Where the **install-sonar-scanner.sh** file is an executable script for installing SonarScanner on Linux-based systems.

On the other hand, the **docker-compose.yml** file is used for installing the images and setting up and starting the containers.

## Instructions
>
> You need to have Git software installed on your system.
>

### Windows

#### Install Desktop

Go to the download page [Docker Desktop](https://www.docker.com/products/docker-desktop/), download, run the file, and follow the instructions.

After restarting the system, as required by the Docker installation, the program will run. (If the software does not start correctly, go to [Troubleshooting](#Troubleshooting)).

#### Run Docker Compose

Next, go to the local Windows disk (usually the `C:` drive), create a folder named *SonarQube*, enter that folder, and in the address bar, type `CMD` to open the command prompt.

Run the following commands:

`git init`

`git pull https://github.com/EARodriguezM/SonarQube-Install`

`docker compose up -d`

The above lines will download the files from this repository into the created folder with the same explained structure, download the SonarQube and PostgreSQL 12 images from Docker repositories, and start the respective containers.

#### Install SonarScanner

>
> The SonarScanner downloaded in this section and in the following link is used when there is no specific scanner for your build system (for JS, TS, Go, Python, PHP, ...). If your system is based on [Maven](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-maven/), [Gradle](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-gradle/), [.NET](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner-for-dotnet/), click on their respective links.
>

Go to the SonarQube documentation with the [SonarScanner](https://docs.sonarsource.com/sonarqube/latest/analyzing-source-code/scanners/sonarscanner/) section and download the **Windows-64-bit** version. This will download a ZIP file that needs to be extracted.

Next, go to the *SonarQube* folder created earlier and create a new folder called **scanner**. Copy all the contents of the ZIP file into the *scanner* folder.

Then, you need to access the environment variable configuration window and **Edit** or **Create** the user variable `Path`, where you add the following path `C:\SonarQube\scanner\bin`, accept the edit to the variable, and close the windows.

#### Configure SonarQube

Open the [local port 9000](http://localhost:9000/) in your browser and log in with the default credentials:

        Username = admin
        Password = admin

After setting a new password as required by the application, the window for creating a new project will appear.

#### Run Analysis: Local

In the window for creating a new project, select *Manually* for manual project creation. Provide a name for the project and a name for the default branch, and the *Project key* will be automatically set by the software.

Next, you will be redirected to the window for analyzing the project, where you will select *Locally*. Generate a new token by clicking on *Generate*, and then click the *Continue* button.

Select the option that describes your system (highly related to the version of SonarScanner you had to install), choose *Windows* as the operating system, and copy the command line that appears in the *Execute the Scanner* section by clicking the *Copy* button.

Open `CMD` in the folder where the root directory of your project is located (where you usually find the node_modules, package.json, lib, src files, among others), and run the copied command.

>
> **NOTE**: Make sure there are no installed dependencies in the folder, i.e., folders like `node_modules`, `build`, among others, should not be present.
>

During the execution, a pop-up window will appear asking for network permissions for Sonar to communicate data between *SonarScanner* and *SonarQube*.

After the execution is finished, the browser will refresh and display the analysis results.


## <a name="Troubleshooting"></a> Troubleshooting
- https://stackoverflow.com/a/68768646
- https://stackoverflow.com/a/61191886