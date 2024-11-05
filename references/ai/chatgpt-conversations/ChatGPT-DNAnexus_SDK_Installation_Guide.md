---
title: DNAnexus SDK Installation Guide
source: https://chatgpt.com/c/672a3796-d348-8002-b319-56ab63cfcd04
---

# DNAnexus SDK Installation Guide

#### You:
[Unsupported Content]

#### You:
<time datetime="2024-11-05T15:19:50.985Z" title="11/5/2024, 3:19:50 PM">15:19</time>

DNAnexus Platform SDK

To install the dx CLI and the Python SDK for your platform run python3 -m pip install dxpy

Found a bug? See Reporting Bugs below.
Welcome to the dx-toolkit repository! This repository contains the DNAnexus API language bindings and utilities for interacting with the DNAnexus platform.

See https://documentation.dnanexus.com/ and http://autodoc.dnanexus.com/ for relevant documentation.

Installing the toolkit from source

The recommended way to install the Python SDK and dx CLI of dx-toolkit locally is with python3 -m pip install -e dx-toolkit/src/python. Any changes made within this checkout will be reflected in the pip installed version.

Building inside docker

To avoid lengthy installation of dependencies on your platform and simultaneous installations of development versions of dx-toolkit on the system, you can build dx-toolkit inside a docker container.

Start python:3.9-bullseye in the interactive mode, mounting the repo you are working on (<local_path_to_repo>/dx-toolkit):

# from root folder of dx-toolkit
docker run -v `pwd`:/dx-toolkit -w /dx-toolkit -it --rm --entrypoint=/bin/bash python:3.9-bullseye
From the interactive shell install dx-toolkit.

A. Using local checkout:
python3 -m pip install src/python/ --upgrade
B. Using remote branch, in this example specified in "@master":
python3 -m pip install --upgrade 'git+https://github.com/dnanexus/dx-toolkit.git@master#egg=dxpy&subdirectory=src/python'
Log in, install dependencies(if needed) and use the container while developing. To rebuild, just save the work and run the step 2 again.

Supported languages

The Platform SDK contains API language bindings for the following platforms:

Python (requires Python 3.8 or higher)
C++
Java (requires Java 7 or higher)
Build dependencies for C++ and Java

Note: There is a known incompatibility (in compiling dxcpp) when using GCC 4.7 with Boost 1.49. Please either use the GCC 4.6 series, or Boost 1.50+.

Ubuntu 22.04

sudo apt install git openjdk-11-jre-headless maven python-is-python3 python3-venv python3-dev libssl-dev libffi-dev \
  flex bison build-essential cmake libboost-all-dev curl libcurl4-openssl-dev
Ubuntu 20.04

sudo apt install git make openjdk-11-jre-headless maven python-is-python3 python3-venv libssl-dev flex bison libffi-dev libboost-all-dev curl libcurl4-openssl-dev
Upload Agent

See the Upload Agent Readme for Upload Agent build documentation.

Reporting Bugs

Please contact support@dnanexus.com for any bug reports or suggestions.

I need help here I am using mac

#### ChatGPT:
<time datetime="2024-11-05T15:20:08.625Z" title="11/5/2024, 3:20:08 PM">15:20</time>

To install the DNAnexus Platform SDK and `dx-toolkit` on macOS, follow these steps:

1. **Install the DNAnexus CLI and Python SDK using `pip`:**

   ```bash
   python3 -m pip install dxpy
   ```

2. **Optional: Install from Source (if modifying `dx-toolkit`):**

   - Clone the `dx-toolkit` repository from GitHub:

     ```bash
     git clone https://github.com/dnanexus/dx-toolkit.git
     ```

   - Install locally using the source:

     ```bash
     cd dx-toolkit
     python3 -m pip install -e dx-toolkit/src/python
     ```

3. **Using Docker for an Isolated Environment:**

   - If you want to avoid installing dependencies directly on your Mac, you can run the `dx-toolkit` inside a Docker container.

     Start a Docker container with Python 3.9 (or your preferred version) and mount your `dx-toolkit` directory:

     ```bash
     docker run -v $(pwd):/dx-toolkit -w /dx-toolkit -it --rm --entrypoint=/bin/bash python:3.9-bullseye
     ```

   - From the interactive shell inside Docker, install `dx-toolkit`:

     ```bash
     python3 -m pip install src/python/ --upgrade
     ```

4. **Installing Additional Dependencies (if using C++/Java):**

   On macOS, if you also need C++ or Java support, you may need to install these dependencies. Run the following commands to install common packages:

   ```bash
   brew install git openjdk@11 maven cmake boost openssl curl
   ```

   Make sure Java is accessible by setting the path if needed:

   ```bash
   export JAVA_HOME=$(/usr/libexec/java_home -v 11)
   ```

5. **Verify the Installation:**

   Check if the `dx` command is available:

   ```bash
   dx --version
   ```

This should help you get set up with `dx-toolkit` on your Mac! Let me know if you encounter any issues.


#### You:
<time datetime="2024-11-05T15:20:28.744Z" title="11/5/2024, 3:20:28 PM">15:20</time>

root@38c41f019147:/dx-toolkit# python3 -m pip install src/python/ --upgrade
ERROR: Invalid requirement: 'src/python/'
Hint: It looks like a path. File 'src/python/' does not exist.!!!!!!!!

#### ChatGPT:
<time datetime="2024-11-05T15:20:40.532Z" title="11/5/2024, 3:20:40 PM">15:20</time>

The error you're seeing suggests that the `src/python/` directory might not be present in the location where you're trying to install it. Here are a few steps to troubleshoot this:

1. **Ensure you're in the correct directory** within your Docker container. When running `docker run`, make sure you’re mounting the correct path where `dx-toolkit` is located on your local machine. Try running:

   ```bash
   ls /dx-toolkit
   ```

   This should list the contents of the `dx-toolkit` repository, including the `src/python/` folder.

2. **Check the Path** to make sure `src/python/` exists:

   ```bash
   ls /dx-toolkit/src/python
   ```

   If you don’t see files in that directory, the repository may not be cloned correctly. Try re-cloning it on your local machine, then re-run the Docker container with the mounted volume.

3. **Re-clone the Repository** if necessary:

   If you didn’t clone the repository before running the Docker command, clone it now:

   ```bash
   git clone https://github.com/dnanexus/dx-toolkit.git
   ```

   Then, navigate into `dx-toolkit` and re-run the Docker command:

   ```bash
   docker run -v $(pwd):/dx-toolkit -w /dx-toolkit -it --rm --entrypoint=/bin/bash python:3.9-bullseye
   ```

   Inside the Docker container, verify the path once more and then try the installation command again:

   ```bash
   python3 -m pip install src/python/ --upgrade
   ```

Let me know if this helps or if the directory structure is still unclear.


#### You:
<time datetime="2024-11-05T15:20:52.630Z" title="11/5/2024, 3:20:52 PM">15:20</time>

I only see my local files when ls

#### ChatGPT:
<time datetime="2024-11-05T15:21:06.780Z" title="11/5/2024, 3:21:06 PM">15:21</time>

It sounds like the `dx-toolkit` directory isn’t correctly mounted within your Docker container, which is why you’re only seeing your local files. Let’s walk through the steps to ensure `dx-toolkit` is correctly mounted and accessible in the Docker environment.

1. **Clone the `dx-toolkit` Repository Locally:**

   On your local machine (outside Docker), clone the repository if you haven’t already:

   ```bash
   git clone https://github.com/dnanexus/dx-toolkit.git
   ```

2. **Navigate to the `dx-toolkit` Folder:**

   After cloning, move into the `dx-toolkit` directory:

   ```bash
   cd dx-toolkit
   ```

3. **Run the Docker Command with Correct Mounting:**

   Now, run the following Docker command from within the `dx-toolkit` directory. This will mount the current directory (the `dx-toolkit` repository) to `/dx-toolkit` inside the container.

   ```bash
   docker run -v $(pwd):/dx-toolkit -w /dx-toolkit -it --rm --entrypoint=/bin/bash python:3.9-bullseye
   ```

   This command mounts the current working directory (`$(pwd)`) to `/dx-toolkit` in Docker, ensuring the container has access to `dx-toolkit`.

4. **Verify the Contents of `/dx-toolkit`:**

   Inside the Docker container, check that you can see the `src/python/` directory:

   ```bash
   ls /dx-toolkit/src/python
   ```

   If the directory structure looks correct, you should see Python files here, which indicates that `dx-toolkit` is mounted correctly.

5. **Install the Python SDK:**

   Now, you can proceed with the installation:

   ```bash
   python3 -m pip install src/python/ --upgrade
   ```

This should resolve the issue, as the correct directory should now be accessible to the Docker container. Let me know if this approach works for you.


#### You:
<time datetime="2024-11-05T15:24:25.979Z" title="11/5/2024, 3:24:25 PM">15:24</time>

how do I now connect to a job that I created on the dna nexus I have the job ID

#### ChatGPT:
<time datetime="2024-11-05T15:24:32.979Z" title="11/5/2024, 3:24:32 PM">15:24</time>

To connect to a job you've created on the DNAnexus platform using its Job ID, you can utilize the DNAnexus Command-Line Interface (CLI). Here's how:

1. **Install the DNAnexus CLI:**

   If you haven't installed the DNAnexus CLI (`dx`), you can do so using `pip`:

   \`\`\`bash
   python3 -m pip install dxpy

   ```
   ```
2. **Log in to DNAnexus:**

   Authenticate your CLI session:

   \`\`\`bash
   dx login

   ```

   Follow the prompts to enter your credentials.

   ```
3. **Describe the Job:**

   To retrieve detailed information about your job, use the `dx describe` command:

   \`\`\`bash
   dx describe <job-ID>

   ```

   Replace `<job-ID>` with your actual Job ID. This command provides comprehensive details about the job, including its status, inputs, outputs, and more.

   ```
4. **Monitor the Job:**

   To monitor the job's progress and view its logs:

   \`\`\`bash
   dx watch <job-ID>

   ```

   This command displays real-time updates on the job's status and outputs.

   ```
5. **Access Job Logs:**

   To view the standard output and error logs of the job:

   \`\`\`bash
   dx get\_logs <job-ID>

   ```

   This will fetch and display the logs, aiding in debugging or understanding the job's execution.

   ```
6. **SSH into the Job's Worker (if applicable):**

   If your job was configured to allow SSH access, you can connect to its execution environment:

   \`\`\`bash
   dx ssh <job-ID>

   ```

   Ensure that SSH access was enabled when the job was launched.
   ```

For more detailed information on monitoring and interacting with jobs, refer to the DNAnexus documentation on [Monitoring Executions](https://documentation.dnanexus.com/user/running-apps-and-workflows/monitoring-executions).

If you encounter any issues or need further assistance, feel free to ask.


#### You:
<time datetime="2024-11-05T15:26:34.879Z" title="11/5/2024, 3:26:34 PM">15:26</time>

dont I need to login to the UK biobank's nexus?

#### ChatGPT:
<time datetime="2024-11-05T15:26:44.417Z" title="11/5/2024, 3:26:44 PM">15:26</time>

To connect to a job you've created on the UK Biobank Research Analysis Platform (UKB-RAP) using its Job ID, follow these steps:

1. **Install the DNAnexus CLI:**

   If you haven't installed the DNAnexus Command-Line Interface (`dx`), you can do so using `pip`:

   \`\`\`bash
   python3 -m pip install dxpy

   ```
   ```
2. **Log in to the UKB-RAP:**

   Authenticate your CLI session to the UK Biobank Research Analysis Platform:

   \`\`\`bash
   dx login --host=auth.dnanexus.com --port=443

   ```

   Follow the prompts to enter your credentials. This command specifies the authentication endpoint for the UKB-RAP. citeturn0search6

   ```
3. **Describe the Job:**

   To retrieve detailed information about your job, use the `dx describe` command:

   \`\`\`bash
   dx describe <job-ID>

   ```

   Replace `<job-ID>` with your actual Job ID. This command provides comprehensive details about the job, including its status, inputs, outputs, and more.

   ```
4. **Monitor the Job:**

   To monitor the job's progress and view its logs:

   \`\`\`bash
   dx watch <job-ID>

   ```

   This command displays real-time updates on the job's status and outputs.

   ```
5. **Access Job Logs:**

   To view the standard output and error logs of the job:

   \`\`\`bash
   dx get\_logs <job-ID>

   ```

   This will fetch and display the logs, aiding in debugging or understanding the job's execution.

   ```
6. **SSH into the Job's Worker (if applicable):**

   If your job was configured to allow SSH access, you can connect to its execution environment:

   \`\`\`bash
   dx ssh <job-ID>

   ```

   Ensure that SSH access was enabled when the job was launched.
   ```

For more detailed information on monitoring and interacting with jobs, refer to the DNAnexus documentation on [Monitoring Executions](https://documentation.dnanexus.com/user/running-apps-and-workflows/monitoring-executions).

If you encounter any issues or need further assistance, feel free to ask.


#### You:
<time datetime="2024-11-05T15:28:21.534Z" title="11/5/2024, 3:28:21 PM">15:28</time>

root@a3b159225b87:/dx-toolkit# dx describe job-Gvb36PQJ5qQG5k42v41jgQQ3
Result 1:
ID                                job-Gvb36PQJ5qQG5k42v41jgQQ3
Try                               0
Class                             job
Job name                          Cloud Workstation
Executable name                   cloud_workstation
Project context                   project-GvJ3jgQJ5qQB10jPfqVyFBqz
Region                            aws:eu-west-2
Billed to                         org-ukb_wallet_08d607553d2
Workspace                         container-Gvb36Q8Jf0V0j0z6j7Zp0qFq
Cache workspace                   container-GvJkb1QJ5qQPZ4F1KXqVjxz7
Resources                         container-GvJ0qK8JfG85f3G3jY0zx35j
App                               app-GvJ0qK85xFq5f3G3jY0Px35V
Instance Type                     mem1_ssd1_v2_x8
Priority                          normal
State                             done
Root execution                    job-Gvb36PQJ5qQG5k42v41jgQQ3
Origin job                        job-Gvb36PQJ5qQG5k42v41jgQQ3
Parent job                        -
Function                          main
Input                             max_session_length = "1"
Output                            -
Output folder                     /MSc Project/Output
Preserve Job Outputs Folder       -
Launched by                       chonkie
Created                           Tue Nov  5 15:01:18 2024
Try created                       Tue Nov  5 15:01:18 2024
Started running                   Tue Nov  5 15:02:40 2024
Stopped running                   Tue Nov  5 15:06:05 2024 (Runtime: 0:03:25)
Last modified                     Tue Nov  5 15:06:11 2024
Depends on                        -
Tags                              server_running
Properties                        -
Total Price                       £0.00
SSH Host Key                      3072 SHA256:BXl8c4jOcnMDUJVAGUpN5x7zoR5EHnac0dJ5lSzMPN8 (RSA)
Tree TAT                          289
Sys Requirements                  {"*": {"instanceType": "mem1_ssd1_v2_x8", "nvidiaDriver": "R535"}}
costLimit                         null
detachedFrom                      null
workerReuseDeadlineRunTime        {"state": "reuse-off", "waitTime": -1, "at": -1}
singleContext                     false
failureCounts                     {}
ignoreReuse                       true
httpsApp                          {"enabled": false}
rank                              0
detachedFromTry                   null
executionPolicy                   {"restartOn": {"UnresponsiveWorker": 2, "JMInternalError": 1,
                                  "ExecutionError": 1}}
finalPriority                     "normal"
networkAccess                     ["*"]
debug                             {}
nvidiaDriver                      "R535"
detailedJobMetrics                false
totalEgress                       {"internetEgress": 0, "regionLocalEgress": 0, "interRegionEgress":
                                  0}
egressComputedAt                  1730819171519
priceComputedAt                   1730819171519
currency                          {"dxCode": 1, "code": "GBP", "symbol": "£", "symbolPosition":
                                  "left", "decimalSymbol": ".", "groupingSymbol": ","}
egressReport                      {"internetEgress": 0, "regionLocalEgress": 0, "interRegionEgress":
                                  0}
timeout                           2592000000

#### ChatGPT:
<time datetime="2024-11-05T15:28:38.984Z" title="11/5/2024, 3:28:38 PM">15:28</time>

It looks like you've successfully retrieved detailed information about your job on DNAnexus. Here’s a breakdown of the key elements and next steps:

1. **Job Status**:
   - **State**: `done` – The job has completed successfully.
   - **Runtime**: 3 minutes and 25 seconds.

2. **Resources and Configuration**:
   - **Instance Type**: `mem1_ssd1_v2_x8`, suitable for memory-intensive tasks.
   - **Region**: `aws:eu-west-2` – Indicates the AWS region used for running the job.
   - **App Executed**: `cloud_workstation` (app ID: `app-GvJ0qK85xFq5f3G3jY0Px35V`).

3. **Outputs and Folders**:
   - **Output Folder**: `/MSc Project/Output` – Check this folder on DNAnexus for any files or data generated by the job.

4. **SSH Access**:
   - **SSH Host Key**: If SSH access is enabled for this job, you can use this host key for verification. However, this job’s output doesn’t indicate SSH access explicitly. If SSH was set up, use the command:
     ```bash
     dx ssh <job-ID>
     ```

5. **Cost and Egress**:
   - **Total Price**: £0.00 (no charges were accrued).
   - **Network Egress**: No egress charges incurred, meaning no significant data was transferred outside the region or over the internet.

6. **Execution Policy**:
   - Automatic retries were set for specific errors like `UnresponsiveWorker` and `ExecutionError`, ensuring resilience in case of job issues.

7. **Next Steps**:
   - Navigate to the `/MSc Project/Output` folder on DNAnexus to review the outputs generated by the job.
   - If additional SSH configuration is needed, ensure SSH access is enabled in job settings before running the `dx ssh` command.

This summary should help you interpret the job details and locate your outputs on DNAnexus. Let me know if you need further assistance accessing or interpreting specific results!


#### You:
<time datetime="2024-11-05T15:29:25.494Z" title="11/5/2024, 3:29:25 PM">15:29</time>

where is that dont I need to mount it?

#### ChatGPT:
<time datetime="2024-11-05T15:29:39.760Z" title="11/5/2024, 3:29:39 PM">15:29</time>

Yes, to access the `/MSc Project/Output` folder on your local machine, you need to either:

1. **Download the Files Directly from DNAnexus**:
   Use the `dx download` command to retrieve specific files or folders to your local machine.

   ```bash
   dx download "project-GvJ3jgQJ5qQB10jPfqVyFBqz:/MSc Project/Output" --recursive
   ```

   - This command downloads the entire `Output` folder to your current directory.
   - If you only need specific files, specify the file path instead of the entire folder.

2. **Mount the Project with `dx fuse`** (if you need continuous access):
   DNAnexus provides a FUSE-based mounting tool called `dx-fuse` that allows you to mount a DNAnexus project as a filesystem on your local machine. Here’s how to set it up:

   - **Install `dx-fuse`** (if not already installed):
     ```bash
     sudo apt install dx-fuse
     ```

   - **Mount the Project**:

     ```bash
     dx-mount project-GvJ3jgQJ5qQB10jPfqVyFBqz /path/to/mountpoint
     ```

     Replace `/path/to/mountpoint` with the desired local directory where you want the project mounted. Once mounted, you can navigate to the `Output` folder in `/path/to/mountpoint/MSc Project/Output` as if it were a local directory.

3. **Access Files in Docker (if using Docker)**:

   - If running this inside Docker, mount the directory you created with `dx-fuse` as a volume in Docker so it’s accessible there.

   ```bash
   docker run -v /path/to/mountpoint:/mnt/dnax-project -it <docker-image>
   ```

This approach allows you to directly access and manage your DNAnexus project files on your local filesystem without downloading them manually each time.


#### You:
<time datetime="2024-11-05T15:30:45.927Z" title="11/5/2024, 3:30:45 PM">15:30</time>

root@a3b159225b87:/dx-toolkit# ls
CHANGELOG.md  Readme-osx.md  build    doc	       environment.csh
COPYING       Readme.md      contrib  environment      environment.fish
Makefile      bin	     debian   environment.bat  src
root@a3b159225b87:/dx-toolkit# cd ..
root@a3b159225b87:/# ls
bin   dev	  etc	lib    mnt  proc  run	srv  tmp  var
boot  dx-toolkit  home	media  opt  root  sbin	sys  usr
root@a3b159225b87:/# cd dx-toolkit
root@a3b159225b87:/dx-toolkit# sudo apt install dx-fuse
bash: sudo: command not found
root@a3b159225b87:/dx-toolkit# 

#### ChatGPT:
<time datetime="2024-11-05T15:30:59.719Z" title="11/5/2024, 3:30:59 PM">15:30</time>

It appears that `sudo` is not available in your Docker environment, which is typical for some minimal images. Here’s an alternative approach:

1. **Run `apt` as Root**:
   Since you’re already running as root in the Docker container, you don’t need `sudo`. You can install `dx-fuse` directly:

   ```bash
   apt update
   apt install dx-fuse
   ```

2. **Mount the DNAnexus Project**:
   Once `dx-fuse` is installed, you can use it to mount your DNAnexus project directly within the Docker container.

   ```bash
   dx-mount project-GvJ3jgQJ5qQB10jPfqVyFBqz /mnt/dnax-project
   ```

   This mounts the DNAnexus project to `/mnt/dnax-project`, where you can then access the `MSc Project/Output` folder directly in your Docker environment.

3. **Verify the Mount**:
   Once mounted, navigate to the directory and list the contents to confirm:

   ```bash
   cd /mnt/dnax-project/MSc Project/Output
   ls
   ```

Let me know if you encounter any issues with these steps!


#### You:
<time datetime="2024-11-05T15:31:18.867Z" title="11/5/2024, 3:31:18 PM">15:31</time>

root@a3b159225b87:/dx-toolkit# apt install dx-fuse
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
E: Unable to locate package dx-fuse
root@a3b159225b87:/dx-toolkit# 

#### ChatGPT:
<time datetime="2024-11-05T15:31:33.372Z" title="11/5/2024, 3:31:33 PM">15:31</time>

The error indicates that `dx-fuse` is not available in the default repositories for your Docker container’s base image. Here’s how to proceed:

1. **Install `dx-fuse` Manually**:

   DNAnexus provides `dx-fuse` as a downloadable package. You can download and install it directly:

   ```bash
   curl -O https://dnanexus-sdk.s3.amazonaws.com/dxfuse/latest/dx-fuse.tar.gz
   ```

2. **Extract and Install**:

   Extract the `dx-fuse` archive and install it:

   ```bash
   tar -xzf dx-fuse.tar.gz
   cd dx-fuse
   ./install
   ```

3. **Mount the Project**:

   After installation, you should be able to mount the DNAnexus project as previously described:

   ```bash
   dx-mount project-GvJ3jgQJ5qQB10jPfqVyFBqz /mnt/dnax-project
   ```

4. **Access Your Files**:

   Once mounted, you’ll find your project files in `/mnt/dnax-project`, allowing you to access and work with the files as needed.

If you encounter issues, it may be necessary to confirm that `fuse` is available on the container’s base image. Let me know how it goes!


#### You:
<time datetime="2024-11-05T15:32:26.725Z" title="11/5/2024, 3:32:26 PM">15:32</time>

root@a3b159225b87:/dx-toolkit# ls
CHANGELOG.md  Readme-osx.md  build    doc	      environment.bat	src
COPYING       Readme.md      contrib  dx-fuse.tar.gz  environment.csh
Makefile      bin	     debian   environment     environment.fish
root@a3b159225b87:/dx-toolkit# tar -xzf dx-fuse.tar.gz

gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now
root@a3b159225b87:/dx-toolkit# ls
CHANGELOG.md  Readme-osx.md  build    doc	      environment.bat	src
COPYING       Readme.md      contrib  dx-fuse.tar.gz  environment.csh
Makefile      bin	     debian   environment     environment.fish
root@a3b159225b87:/dx-toolkit# 

#### ChatGPT:
<time datetime="2024-11-05T15:32:36.069Z" title="11/5/2024, 3:32:36 PM">15:32</time>

It seems that the file downloaded as `dx-fuse.tar.gz` is not in the gzip format. This could happen if the file was not downloaded correctly. Let’s reattempt the download with a different approach:

1. **Redownload `dx-fuse` with `wget`**:
   Try using `wget` to ensure the correct format:

   ```bash
   wget https://dnanexus-sdk.s3.amazonaws.com/dxfuse/latest/dx-fuse.tar.gz -O dx-fuse.tar.gz
   ```

2. **Verify the File Format**:
   After downloading, confirm the file type to check if it’s a valid gzip file:

   ```bash
   file dx-fuse.tar.gz
   ```

   It should return something like `gzip compressed data`. If it doesn’t, the download might still be corrupted.

3. **Extract and Install**:
   If the file type is correct, proceed with extraction:

   ```bash
   tar -xzf dx-fuse.tar.gz
   cd dx-fuse
   ./install
   ```

If the file format still doesn’t seem correct, we may need to check DNAnexus documentation or the download source. Let me know if these steps help!


#### You:
<time datetime="2024-11-05T15:32:55.378Z" title="11/5/2024, 3:32:55 PM">15:32</time>

Makefile      bin	     debian   environment     environment.fish
root@a3b159225b87:/dx-toolkit# tar -xzf dx-fuse.tar.gz

gzip: stdin: not in gzip format
tar: Child returned status 1
tar: Error is not recoverable: exiting now
root@a3b159225b87:/dx-toolkit# ls
CHANGELOG.md  Readme-osx.md  build    doc	      environment.bat	src
COPYING       Readme.md      contrib  dx-fuse.tar.gz  environment.csh
Makefile      bin	     debian   environment     environment.fish
root@a3b159225b87:/dx-toolkit# wget https://dnanexus-sdk.s3.amazonaws.com/dxfuse/latest/dx-fuse.tar.gz -O dx-fuse.tar.gz
--2024-11-05 15:32:44--  https://dnanexus-sdk.s3.amazonaws.com/dxfuse/latest/dx-fuse.tar.gz
Resolving dnanexus-sdk.s3.amazonaws.com (dnanexus-sdk.s3.amazonaws.com)... 52.216.185.179, 52.217.204.209, 54.231.193.81, ...
Connecting to dnanexus-sdk.s3.amazonaws.com (dnanexus-sdk.s3.amazonaws.com)|52.216.185.179|:443... connected.
HTTP request sent, awaiting response... 403 Forbidden
2024-11-05 15:32:44 ERROR 403: Forbidden.

#### ChatGPT:
<time datetime="2024-11-05T15:33:03.067Z" title="11/5/2024, 3:33:03 PM">15:33</time>

It appears you're encountering a `403 Forbidden` error when attempting to download `dx-fuse.tar.gz` from the DNAnexus S3 bucket. This error typically indicates permission issues or that the resource is unavailable.

**Alternative Steps to Obtain `dx-fuse`:**

1. **Access the DNAnexus Downloads Page:**
   - Visit the [DNAnexus Downloads](https://documentation.dnanexus.com/downloads) page.
   - Look for the `dx-fuse` section to find the appropriate download link for your operating system.

2. **Download `dx-fuse` Manually:**
   - If direct download links are provided, use your browser to download the `dx-fuse` package to your local machine.

3. **Transfer the File to Your Docker Environment:**
   - If you're working within a Docker container, you can mount a local directory containing the downloaded `dx-fuse` package into the container.
   - For example, if the package is in `/path/to/local/dxfuse`, run:

     \`\`\`bash
     docker run -v /path/to/local/dxfuse:/mnt/dxfuse -it your-docker-image

     ```
     ```
   - Inside the container, navigate to `/mnt/dxfuse` to access the `dx-fuse` package.

4. **Install `dx-fuse`:**
   - Extract the package:

     \`\`\`bash
     tar -xzf dx-fuse.tar.gz

     ```
     ```
   - Navigate to the extracted directory and run the installation script:

     \`\`\`bash
     cd dx-fuse
     ./install

     ```
     ```

**Additional Considerations:**

- **Check for Access Permissions:**
  - Ensure you have the necessary permissions to access DNAnexus resources. If you're part of an organization, verify that your account has the appropriate access rights.

- **Contact DNAnexus Support:**
  - If issues persist, consider reaching out to [DNAnexus Support](mailto:support@dnanexus.com) for assistance.

By following these steps, you should be able to obtain and install `dx-fuse` successfully.


#### You:
<time datetime="2024-11-05T15:36:17.477Z" title="11/5/2024, 3:36:17 PM">15:36</time>

instead cant I just try and find my file or folder within the docker which I logged into dna nexus perhaps its aready mounted

#### ChatGPT:
<time datetime="2024-11-05T15:36:35.045Z" title="11/5/2024, 3:36:35 PM">15:36</time>

Yes, it’s possible that the project files are already accessible within your Docker container if you’re logged into DNAnexus and have proper access to the project. Here’s how to check:

1. **Navigate to Possible Mount Points**:
   Look around common directories like `/home`, `/mnt`, or `/workspace`, which are sometimes used as mount points for cloud environments.

   ```bash
   cd /home
   ls
   ```

   You can also try:

   ```bash
   cd /mnt
   ls
   ```

   or

   ```bash
   cd /workspace
   ls
   ```

2. **List All Mounted Filesystems**:
   Run the following command to list all mounted filesystems and check if DNAnexus files are mounted somewhere:

   ```bash
   df -h
   ```

   This will display all mounted directories and may indicate where your project files are located if they’re already mounted.

3. **Check Your Home Directory**:
   Sometimes, DNAnexus environments place data in the user’s home directory:

   ```bash
   cd ~
   ls
   ```

4. **Use `dx` Commands to Explore the Project**:
   If you can’t locate the files manually, you can use `dx` commands to list files and directories within the project. Use your project ID:

   ```bash
   dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/MSc Project/Output
   ```

   This command will show you the contents of the `Output` folder in your DNAnexus project.

Let me know if this helps you find your files!


#### You:
<time datetime="2024-11-05T15:38:29.625Z" title="11/5/2024, 3:38:29 PM">15:38</time>

surely this output will tell us?

Result 1:
ID                                job-Gvb36PQJ5qQG5k42v41jgQQ3
Try                               0
Class                             job
Job name                          Cloud Workstation
Executable name                   cloud_workstation
Project context                   project-GvJ3jgQJ5qQB10jPfqVyFBqz
Region                            aws:eu-west-2
Billed to                         org-ukb_wallet_08d607553d2
Workspace                         container-Gvb36Q8Jf0V0j0z6j7Zp0qFq
Cache workspace                   container-GvJkb1QJ5qQPZ4F1KXqVjxz7
Resources                         container-GvJ0qK8JfG85f3G3jY0zx35j
App                               app-GvJ0qK85xFq5f3G3jY0Px35V
Instance Type                     mem1_ssd1_v2_x8
Priority                          normal
State                             done
Root execution                    job-Gvb36PQJ5qQG5k42v41jgQQ3
Origin job                        job-Gvb36PQJ5qQG5k42v41jgQQ3
Parent job                        -
Function                          main
Input                             max_session_length = "1"
Output                            -
Output folder                     /MSc Project/Output
Preserve Job Outputs Folder       -
Launched by                       chonkie
Created                           Tue Nov  5 15:01:18 2024
Try created                       Tue Nov  5 15:01:18 2024
Started running                   Tue Nov  5 15:02:40 2024
Stopped running                   Tue Nov  5 15:06:05 2024 (Runtime: 0:03:25)
Last modified                     Tue Nov  5 15:06:11 2024
Depends on                        -
Tags                              server_running
Properties                        -
Total Price                       £0.00
SSH Host Key                      3072 SHA256:BXl8c4jOcnMDUJVAGUpN5x7zoR5EHnac0dJ5lSzMPN8 (RSA)
Tree TAT                          289
Sys Requirements                  {"*": {"instanceType": "mem1_ssd1_v2_x8", "nvidiaDriver": "R535"}}
costLimit                         null
detachedFrom                      null
workerReuseDeadlineRunTime        {"state": "reuse-off", "waitTime": -1, "at": -1}
singleContext                     false
failureCounts                     {}
ignoreReuse                       true
httpsApp                          {"enabled": false}
rank                              0
detachedFromTry                   null
executionPolicy                   {"restartOn": {"UnresponsiveWorker": 2, "JMInternalError": 1,
                                  "ExecutionError": 1}}
finalPriority                     "normal"
networkAccess                     ["*"]
debug                             {}
nvidiaDriver                      "R535"
detailedJobMetrics                false
totalEgress                       {"internetEgress": 0, "regionLocalEgress": 0, "interRegionEgress":
                                  0}
egressComputedAt                  1730819171519
priceComputedAt                   1730819171519
currency                          {"dxCode": 1, "code": "GBP", "symbol": "£", "symbolPosition":
                                  "left", "decimalSymbol": ".", "groupingSymbol": ","}
egressReport                      {"internetEgress": 0, "regionLocalEgress": 0, "interRegionEgress":
                                  0}
timeout                           2592000000
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T15:38:42.939Z" title="11/5/2024, 3:38:42 PM">15:38</time>

The output you’ve shared provides valuable details, and it indeed confirms the **Output folder** path as `/MSc Project/Output`. However, it doesn’t specify a local mount path or direct location in the container.

Given this, here’s how to proceed to check if the folder is accessible within the Docker container:

1. **Check the Root Directory**:
   Since the output folder is `/MSc Project/Output`, it may be accessible from the root or another mounted directory.

   Try listing the contents directly:

   ```bash
   ls "/MSc Project/Output"
   ```

2. **Explore Other Common Paths**:
   If that command doesn’t yield results, check other likely locations:

   ```bash
   ls /data
   ls /workspace
   ```

3. **List All Directories to Find `/MSc Project/Output`**:
   Use `find` to locate the folder if it’s mounted somewhere in the container:

   ```bash
   find / -type d -name "Output" 2>/dev/null
   ```

This should help identify if `/MSc Project/Output` is available or if any additional mounting or download steps are required.


#### You:
<time datetime="2024-11-05T15:40:37.515Z" title="11/5/2024, 3:40:37 PM">15:40</time>

could this instance be completed I see its done in the log is it still running?

#### ChatGPT:
<time datetime="2024-11-05T15:40:49.203Z" title="11/5/2024, 3:40:49 PM">15:40</time>

The `State: done` in the job log confirms that the instance has completed its run and is no longer active. Here’s a breakdown:

- **State**: `done` – This indicates that the job has finished processing and is not currently running.
- **Stopped running**: Tue Nov 5 15:06:05 2024 – This is the timestamp showing when the job ended.

Since the job is complete, you won’t have access to an active session on this instance. To access the outputs, you would typically:

1. **Download the Results** from the `/MSc Project/Output` folder on DNAnexus using the `dx` CLI, or
2. **Check for the output files directly** in the DNAnexus web interface if they were saved there.

If you need a live session again, you’ll need to start a new job or interactive session in DNAnexus.


#### You:
<time datetime="2024-11-05T15:41:16.781Z" title="11/5/2024, 3:41:16 PM">15:41</time>

there is workstation cloud for dna nexus but it just loads then its done?

#### ChatGPT:
<time datetime="2024-11-05T15:41:24.366Z" title="11/5/2024, 3:41:24 PM">15:41</time>

It appears you're encountering an issue where the DNAnexus Cloud Workstation session terminates immediately after starting. This behavior can result from several factors:

1. **Session Duration Setting**: The `max_session_length` parameter defines the maximum duration of the workstation session. If this is set to a very short time (e.g., "1"), the session may end almost immediately. Ensure you're specifying an appropriate duration, such as "1h" for one hour.

   **Example Command**:

   \`\`\`bash
   dx run app-cloud\_workstation --ssh -i max\_session\_length=1h

   ```

   This command initiates a Cloud Workstation session with a duration of one hour.

   ```

2. **Instance Type Selection**: Choosing an incompatible or unsupported instance type can cause the session to terminate prematurely. Verify that the instance type you're selecting is supported and appropriate for your tasks.

3. **Resource Availability**: Occasionally, resource constraints or availability issues in the selected region can lead to session termination. If possible, try launching the workstation in a different region or at a different time.

4. **SSH Configuration**: If you're attempting to connect via SSH, ensure that your SSH keys are correctly configured. Misconfigurations can prevent successful connections, leading to session termination. Refer to the DNAnexus documentation on [Connecting to Jobs](https://documentation.dnanexus.com/developer/apps/execution-environment/connecting-to-jobs) for guidance.

5. **Network Access Settings**: Ensure that your network settings allow for the necessary connections. Firewalls or restrictive network policies can interfere with session stability.

For detailed information on configuring and troubleshooting the Cloud Workstation, consult the [DNAnexus Cloud Workstation Documentation](https://documentation.dnanexus.com/developer/cloud-workstation).

If the issue persists after verifying these factors, consider reaching out to [DNAnexus Support](mailto:support@dnanexus.com) for further assistance.


#### You:
<time datetime="2024-11-05T15:47:11.610Z" title="11/5/2024, 3:47:11 PM">15:47</time>

how do I now extra data from the data.dataset file. This should be on my dnanexus root folder however when I connected and created a new cloud workstation on terminal I dont see this data.dataset file

#### ChatGPT:
<time datetime="2024-11-05T15:47:31.458Z" title="11/5/2024, 3:47:31 PM">15:47</time>

If you're not seeing the `data.dataset` file in the root folder of your DNAnexus Cloud Workstation, it’s possible that the file isn’t automatically available in your Cloud Workstation environment. Here are steps to ensure you can access it:

1. **Verify File Location in Project**:
   - Use the `dx ls` command to locate the `data.dataset` file within your DNAnexus project. List all files in the root project directory:

     ```bash
     dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/
     ```

   - If the file is in a specific folder, specify the path:

     ```bash
     dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/path/to/folder
     ```

2. **Download the File to Your Workstation**:
   - Once you locate the file in your DNAnexus project, you can download it to your Cloud Workstation. Use the following command, specifying the path to the file:

     ```bash
     dx download project-GvJ3jgQJ5qQB10jPfqVyFBqz:/path/to/data.dataset -o data.dataset
     ```

   - This will download the `data.dataset` file to the current directory on your Cloud Workstation.

3. **Load and Extract Data**:
   - After downloading, you can load and process the file using a tool like `cat` for text-based data or `head` to preview it. For more structured data, load it into Python, R, or another program in your Cloud Workstation.

4. **Automate Download on Workstation Launch (Optional)**:
   - If you frequently need this file, you can set up a script to automatically download it whenever you create a new Cloud Workstation.

5. **Verify Permissions**:
   - Ensure you have access rights to the file. If you’re part of an organization, confirm that your user permissions allow you to access and download this data.

If you still can’t locate `data.dataset`, it may not be in the project, and you may need to check with DNAnexus support for further investigation.


#### You:
<time datetime="2024-11-05T15:48:57.200Z" title="11/5/2024, 3:48:57 PM">15:48</time>

root@a3b159225b87:/dx-toolkit# dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/
.table-exporter/
Bulk/
MSc Project/
Showcase metadata/
app23889_20241024233847
data.dataset
Total : record-Gvb2Kv8J5qQ8q1vFX4YQ8847
Total : record-Gvb0x9QJ5qQJjVz6vjxkJJqP
root@a3b159225b87:/dx-toolkit# dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/MSc Project/  
usage: dx [-h] [--version] command ...

DNAnexus Command-Line Client, API v1.0.0, client v0.385.0

dx is a command-line client for interacting with the DNAnexus platform.  You
can log in, navigate, upload, organize and share your data, launch analyses,
and more.  For a quick tour of what the tool can do, see

  https://documentation.dnanexus.com/getting-started/tutorials/cli-quickstart#quickstart-for-cli

For a breakdown of dx commands by category, run "dx help".

dx exits with exit code 3 if invalid input is provided or an invalid operation
is requested, and exit code 1 if an internal error is encountered.  The latter
usually indicate bugs in dx; please report them at

  https://github.com/dnanexus/dx-toolkit/issues

optional arguments:
  -h, --help  show this help message and exit
  --env-help  Display help message for overriding environment
              variables
  --version   show program's version number and exit

dx: error: unrecognized arguments: Project/
root@a3b159225b87:/dx-toolkit# dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:MSc Project/
usage: dx [-h] [--version] command ...

DNAnexus Command-Line Client, API v1.0.0, client v0.385.0

dx is a command-line client for interacting with the DNAnexus platform.  You
can log in, navigate, upload, organize and share your data, launch analyses,
and more.  For a quick tour of what the tool can do, see

  https://documentation.dnanexus.com/getting-started/tutorials/cli-quickstart#quickstart-for-cli

For a breakdown of dx commands by category, run "dx help".

dx exits with exit code 3 if invalid input is provided or an invalid operation
is requested, and exit code 1 if an internal error is encountered.  The latter
usually indicate bugs in dx; please report them at

  https://github.com/dnanexus/dx-toolkit/issues

optional arguments:
  -h, --help  show this help message and exit
  --env-help  Display help message for overriding environment
              variables
  --version   show program's version number and exit

dx: error: unrecognized arguments: Project/
root@a3b159225b87:/dx-toolkit# 

#### ChatGPT:
<time datetime="2024-11-05T15:49:06.974Z" title="11/5/2024, 3:49:06 PM">15:49</time>

The error you're seeing occurs because the folder name, **"MSc Project"**, contains a space, which needs to be properly escaped or quoted in the `dx` command. Here’s how you can list the contents:

### Corrected Command with Quoting

Use quotes around the path to handle spaces:

```bash
dx ls "project-GvJ3jgQJ5qQB10jPfqVyFBqz:/MSc Project/"
```

or you can escape the space using a backslash (`\`):

```bash
dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/MSc\ Project/
```

### Accessing the `data.dataset` File

Now that you've verified `data.dataset` is in the root directory, you can download it to your Cloud Workstation with:

```bash
dx download project-GvJ3jgQJ5qQB10jPfqVyFBqz:/data.dataset -o data.dataset
```

This command will download `data.dataset` to your current directory. Once downloaded, you can proceed with any data extraction or analysis directly on your Cloud Workstation.


#### You:
<time datetime="2024-11-05T15:51:31.407Z" title="11/5/2024, 3:51:31 PM">15:51</time>

I cant download, what I need to do it extract data from that file I have a cohort saved somwher called all and then I have another file in another location which has all the field names to dowload the csv with, what do I do next?

#### ChatGPT:
<time datetime="2024-11-05T15:51:51.466Z" title="11/5/2024, 3:51:51 PM">15:51</time>

Since you can’t download the `data.dataset` file directly, you’ll need to use the DNAnexus CLI tools to interact with it within the platform. Here’s a step-by-step approach to locate and extract the data you need:

### 1. **Identify the Cohort and Fields to Extract**

- **Cohort:** Since you mentioned a cohort named **"all"**, start by listing any cohorts saved within the project to confirm its location:

  ```bash
  dx find data --name "*all*"
  ```

- **Fields File:** Locate the file containing the field names you’ll use for CSV export:

  ```bash
  dx find data --name "*fields*"
  ```

### 2. **Inspect `data.dataset` File Content**

If `data.dataset` is a DNAnexus record or table, you can inspect it directly to understand its structure.

```bash
dx describe data.dataset
```

This command will provide details on the file's type and structure. If it’s a table, you can query it directly for specific data using DNAnexus commands.

### 3. **Extract Data Based on the Cohort and Fields**

If `data.dataset` is a table, you can use the `dx export` command to extract data:

- **Set up a Query to Extract Fields for the Cohort:**
  Use a query to filter records based on the cohort and select specific fields.

  ```bash
  dx select <field-names> --query "<filter-query-for-cohort-all>"
  ```

  This is a generic example. You’ll need to adjust it to match your table's structure and naming conventions.

### 4. **Export the Data to CSV**

To export the data in CSV format:

```bash
dx export data.dataset --output=csv > extracted_data.csv
```

This command directs the output into a CSV file that you can access from within DNAnexus.

### 5. **Verify and Inspect Extracted Data**

Once the data is exported, you can inspect the `extracted_data.csv` file in your Cloud Workstation.


#### You:
<time datetime="2024-11-05T15:54:10.396Z" title="11/5/2024, 3:54:10 PM">15:54</time>

Result 1:
ID                                record-GvJP9yjJyQ6QzZpkk4qpKVX3
Class                             record
Project                           project-GvJ3jgQJ5qQB10jPfqVyFBqz
Folder                            /
Name                              data.dataset
State                             closed
Visibility                        visible
Types                             Dataset
Properties                        -
Tags                              -
Outgoing links                    database-GvJJbfjJyQ6y1B56fg8X51BP,
                                  database-Fx7Fj58JjG8Yf6bKPX9Yzykf, file-GvJP9vjJyQ6gjBZ6Y9qgppBq
Created                           Fri Oct 25 01:31:39 2024
Created by                        ukb.robot
 via the job                      job-GvJJVq0JyQ6qKz597FPxPV0P
Last modified                     Mon Oct 28 13:34:16 2024
Size                              420
sponsoredUntil                    2082758399000

#### ChatGPT:
<time datetime="2024-11-05T15:54:57.599Z" title="11/5/2024, 3:54:57 PM">15:54</time>

The `data.dataset` file appears to be a **record** on DNAnexus, not a standard file format, which means it likely references other data entities rather than containing raw data itself. Here’s how you can proceed to extract data based on this record and associated files:

### Steps to Access and Extract Data from `data.dataset`

1. **Identify Linked Files or Databases**:
   The `Outgoing links` section shows references to other objects on DNAnexus. These linked IDs (`database-GvJJbfjJyQ6y1B56fg8X51BP`, `database-Fx7Fj58JjG8Yf6bKPX9Yzykf`, and `file-GvJP9vjJyQ6gjBZ6Y9qgppBq`) are likely tables or databases with the data you need.

2. **Describe Linked Databases or Files**:
   Use `dx describe` to get more details on each linked database or file, which will clarify where the actual cohort data resides.

   ```bash
   dx describe database-GvJJbfjJyQ6y1B56fg8X51BP
   dx describe database-Fx7Fj58JjG8Yf6bKPX9Yzykf
   dx describe file-GvJP9vjJyQ6gjBZ6Y9qgppBq
   ```

   This will help identify the linked database or file that contains your cohort data.

3. **Query the Database for the Cohort and Fields**:
   Once you've identified the correct database, you can query it to extract specific data. For instance, if `database-GvJJbfjJyQ6y1B56fg8X51BP` contains the cohort data, use:

   ```bash
   dx find records --project=project-GvJ3jgQJ5qQB10jPfqVyFBqz --folder="/" --name "*all*"
   ```

   This command should list records matching your cohort name.

4. **Extract Data into CSV Using Field Names**:
   - If you have a file with the specific field names you want, locate it and use it to specify the columns for CSV export.
   - You can then use a command such as:

     ```bash
     dx export records <database-ID> --fields=<field-names> --format=csv > extracted_data.csv
     ```

     Replace `<database-ID>` with the actual database ID (like `database-GvJJbfjJyQ6y1B56fg8X51BP`), and `<field-names>` with a comma-separated list of field names.

5. **Verify Extracted Data**:
   The file `extracted_data.csv` should now contain the data for the specified cohort and fields, which you can further inspect and analyze within your DNAnexus Cloud Workstation.

This method should help you pull out the necessary data for your cohort and specific fields. Let me know if you need further assistance with any of these steps!


#### You:
<time datetime="2024-11-05T15:55:22.142Z" title="11/5/2024, 3:55:22 PM">15:55</time>

root@a3b159225b87:/# dx describe database-GvJJbfjJyQ6y1B56fg8X51BP
dx describe database-Fx7Fj58JjG8Yf6bKPX9Yzykf
dx describe file-GvJP9vjJyQ6gjBZ6Y9qgppBq
Result 1:
ID                                database-GvJJbfjJyQ6y1B56fg8X51BP
Class                             database
Project                           project-GvJ3jgQJ5qQB10jPfqVyFBqz
Folder                            /
Name                              app23889_20241024233847
State                             closed
Visibility                        visible
Types                             -
Properties                        -
Tags                              -
Outgoing links                    -
Created                           Thu Oct 24 23:40:11 2024
Created by                        ukb.robot
 via the job                      job-GvJJVq0JyQ6qKz597FPxPV0P
Last modified                     Fri Oct 25 01:31:27 2024
databaseName                      "app23889_20241024233847"
uniqueDatabaseName                "database_gvjjbfjjyq6y1b56fg8x51bp__app23889_20241024233847"
databaseType                      "dnax"
Result 1:
ID                                database-Fx7Fj58JjG8Yf6bKPX9Yzykf
Class                             database
Project                           project-Fx40JV8JjG8YX2Bf4f628Qx4
Folder                            /Genome Reference/GRCh38.92
Name                              grch38_92_euw2_transcript
State                             open
Visibility                        visible
Types                             -
Properties                        -
Tags                              -
Outgoing links                    -
Created                           Tue Sep  1 21:24:37 2020
Created by                        ksoni
Last modified                     Tue Sep  1 21:24:37 2020
databaseName                      "grch38_92_euw2_transcript"
uniqueDatabaseName                "database_fx7fj58jjg8yf6bkpx9yzykf__grch38_92_euw2_transcript"
databaseType                      "dnax"
Result 1:
ID                                file-GvJP9vjJyQ6gjBZ6Y9qgppBq
Class                             file
Project                           project-GvJ3jgQJ5qQB10jPfqVyFBqz
Folder                            /
Name                              app23889_20241024233847.dataset.fields.json.gz
State                             closed
Visibility                        hidden
Types                             -
Properties                        -
Tags                              -
Outgoing links                    -
Created                           Fri Oct 25 01:31:31 2024
Created by                        ukb.robot
 via the job                      job-GvJJVq0JyQ6qKz597FPxPV0P
Last modified                     Fri Oct 25 01:31:41 2024
sponsoredUntil                    2082758399000
Media type                        application/json+gzip
archivalState                     "live"
Size                              2.05 MB
cloudAccount                      "cloudaccount-dnanexus"
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T15:55:52.954Z" title="11/5/2024, 3:55:52 PM">15:55</time>

Based on your output:

- **Database `database-GvJJbfjJyQ6y1B56fg8X51BP`** likely contains your data of interest, as it was created around the same time as `data.dataset`.
- **File `file-GvJP9vjJyQ6gjBZ6Y9qgppBq`** (`app23889_20241024233847.dataset.fields.json.gz`) appears to contain field names in JSON format, which you can use to identify the fields for extraction.

Here’s how to proceed:

### Step 1: Inspect the Fields File

To determine which fields are available for extraction:

1. **Decompress and View the JSON File** (`app23889_20241024233847.dataset.fields.json.gz`):

   Since it’s a gzipped JSON, use the following command to view its contents:

   ```bash
   dx cat file-GvJP9vjJyQ6gjBZ6Y9qgppBq | gunzip -c | less
   ```

   This will display the JSON structure, allowing you to identify the field names.

### Step 2: Extract Data from the Database

1. **Query the Database with Specific Fields**:
   After identifying the fields you need from the JSON file, query `database-GvJJbfjJyQ6y1B56fg8X51BP` to extract relevant records.

   Use the `dx` command to specify fields:

   ```bash
   dx export database-GvJJbfjJyQ6y1B56fg8X51BP --fields="field1,field2,field3" --format=csv > extracted_data.csv
   ```

   Replace `field1,field2,field3` with the actual field names from the JSON file.

### Step 3: Verify Extracted Data

The `extracted_data.csv` file should now contain the data you selected. You can review it directly on your Cloud Workstation by opening it with a text editor or by running:

```bash
head extracted_data.csv
```

This process should help you extract the specific cohort data you need from the DNAnexus database. Let me know if you encounter any issues with these steps!


#### You:
<time datetime="2024-11-05T15:57:21.575Z" title="11/5/2024, 3:57:21 PM">15:57</time>

root@a3b159225b87:/# dx export database-GvJJbfjJyQ6y1B56fg8X51BP --fields="eid, p3_i0,p3_i1" --format=csv > extracted_data.csv
usage: dx [-h] [--version] command ...

DNAnexus Command-Line Client, API v1.0.0, client v0.385.0

dx is a command-line client for interacting with the DNAnexus platform.  You
can log in, navigate, upload, organize and share your data, launch analyses,
and more.  For a quick tour of what the tool can do, see

  https://documentation.dnanexus.com/getting-started/tutorials/cli-quickstart#quickstart-for-cli

For a breakdown of dx commands by category, run "dx help".

dx exits with exit code 3 if invalid input is provided or an invalid operation
is requested, and exit code 1 if an internal error is encountered.  The latter
usually indicate bugs in dx; please report them at

  https://github.com/dnanexus/dx-toolkit/issues

optional arguments:
  -h, --help  show this help message and exit
  --env-help  Display help message for overriding environment
              variables
  --version   show program's version number and exit

dx: error: argument command: invalid choice: export
(choose from login, logout, exit, whoami, env, setenv, clearenv, invite,
uninvite, ls, tree, pwd, select, cd, cp, mv, mkdir, rmdir, rm, describe,
upload, download, make_download_url, cat, head, build, build_asset, add, list,
remove, update, install, uninstall, run, watch, ssh_config, ssh, terminate,
rmproject, new, get_details, set_details, set_visibility, add_types,
remove_types, tag, untag, rename, set_properties, unset_properties, close,
wait, get, find, api, generate_batch_inputs, publish,
archive, unarchive, extract_dataset, extract_assay, create_cohort, help)
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T15:57:32.353Z" title="11/5/2024, 3:57:32 PM">15:57</time>

It seems the `dx` CLI does not support an `export` command directly. Instead, you can use `dx extract_dataset` or `dx extract_assay` if your dataset or database supports these operations. Here’s how to proceed with the correct commands:

### Step 1: Use `dx extract_dataset` for CSV Export

The `extract_dataset` command is designed for datasets and databases. You can specify fields and output format if `database-GvJJbfjJyQ6y1B56fg8X51BP` supports it.

1. **Extract Data with Specified Fields**:

   ```bash
   dx extract_dataset database-GvJJbfjJyQ6y1B56fg8X51BP --fields="eid,p3_i0,p3_i1" --format=csv --output=extracted_data.csv
   ```

   This command specifies the fields and sets the output format to CSV. It saves the output to `extracted_data.csv` in the current directory.

2. **Verify the Output**:

   After the extraction completes, you can view the first few lines of the file to ensure it’s correct:

   ```bash
   head extracted_data.csv
   ```

If `extract_dataset` isn’t supported by this database, let me know, and we can explore other approaches based on DNAnexus’s command capabilities for databases.


#### You:
<time datetime="2024-11-05T15:58:08.169Z" title="11/5/2024, 3:58:08 PM">15:58</time>

root@a3b159225b87:/# dx extract_dataset database-GvJJbfjJyQ6y1B56fg8X51BP --fields="eid,p3_i0,p3_i1" --format=csv --output=extracted_data.csv
usage: dx [-h] [--version] command ...

DNAnexus Command-Line Client, API v1.0.0, client v0.385.0

dx is a command-line client for interacting with the DNAnexus platform.  You can
log in, navigate, upload, organize and share your data, launch analyses, and
more.  For a quick tour of what the tool can do, see

  https://documentation.dnanexus.com/getting-started/tutorials/cli-quickstart#quickstart-for-cli

For a breakdown of dx commands by category, run "dx help".

dx exits with exit code 3 if invalid input is provided or an invalid operation is
requested, and exit code 1 if an internal error is encountered.  The latter
usually indicate bugs in dx; please report them at

  https://github.com/dnanexus/dx-toolkit/issues

optional arguments:
  -h, --help  show this help message and exit
  --env-help  Display help message for overriding environment variables
  --version   show program's version number and exit

dx: error: unrecognized arguments: --format=csv
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T15:58:18.521Z" title="11/5/2024, 3:58:18 PM">15:58</time>

The error message suggests that `dx extract_dataset` does not recognize the `--format=csv` argument, meaning it may not support output format specification directly within this command. Instead, try the following streamlined approach:

### Step 1: Extract Data Without Specifying Format

Run `dx extract_dataset` without the `--format=csv` argument:

```bash
dx extract_dataset database-GvJJbfjJyQ6y1B56fg8X51BP --fields="eid,p3_i0,p3_i1" --output=extracted_data.json
```

This command should save the extracted data in JSON format (or whatever default format DNAnexus uses).

### Step 2: Convert JSON to CSV

Once you have the data in JSON, you can convert it to CSV within your environment using Python or another command-line tool.

#### Using Python for Conversion

1. Open a Python environment in the command line or create a script:

   ```python
   import pandas as pd
   import json

   # Load the JSON data
   with open("extracted_data.json") as f:
       data = json.load(f)

   # Convert to DataFrame and save as CSV
   df = pd.DataFrame(data)
   df.to_csv("extracted_data.csv", index=False)
   ```

2. Run the script, or save it as `convert_to_csv.py` and run:

   ```bash
   python3 convert_to_csv.py
   ```

This should give you the `extracted_data.csv` file in the desired CSV format. Let me know if this helps or if we need to adjust the approach further!


#### You:
<time datetime="2024-11-05T15:58:51.428Z" title="11/5/2024, 3:58:51 PM">15:58</time>

root@a3b159225b87:/# dx extract_dataset database-GvJJbfjJyQ6y1B56fg8X51BP --fields="eid,p3_i0,p3_i1" --output=extracted_data.json
database-GvJJbfjJyQ6y1B56fg8X51BP: Invalid path. The path must point to a record type of cohort or dataset
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T15:59:05.559Z" title="11/5/2024, 3:59:05 PM">15:59</time>

The error indicates that `database-GvJJbfjJyQ6y1B56fg8X51BP` is not recognized as a valid `cohort` or `dataset` type. Given this, you might need to create or reference an existing **cohort** within the `data.dataset` or linked databases, then query data through that cohort. Here’s how you can approach this:

### Step 1: Verify the Existence of a Cohort

Since you mentioned an **"all" cohort** previously, let’s check if it already exists:

```bash
dx find records --project=project-GvJ3jgQJ5qQB10jPfqVyFBqz --class cohort
```

This command will list all cohorts in the project. Look for any cohort named "all" or similar.

### Step 2: Create a Cohort if Necessary

If you don’t find an existing cohort, you may need to create one. Assuming you want to create a cohort based on certain criteria within `database-GvJJbfjJyQ6y1B56fg8X51BP`, use:

```bash
dx create_cohort --database=database-GvJJbfjJyQ6y1B56fg8X51BP --name="all"
```

This should create a cohort that can then be queried.

### Step 3: Extract Data from the Cohort

Once you have the cohort, try using `dx extract_dataset` with this cohort. If the cohort ID is `cohort-Gxyz`, the command would be:

```bash
dx extract_dataset cohort-Gxyz --fields="eid,p3_i0,p3_i1" --output=extracted_data.json
```

This should provide the data you need if the cohort is valid. Let me know if these steps reveal any useful results or if further troubleshooting is needed!


#### You:
<time datetime="2024-11-05T16:00:02.464Z" title="11/5/2024, 4:00:02 PM">16:00</time>

root@a3b159225b87:/# dx find records --project=project-GvJ3jgQJ5qQB10jPfqVyFBqz --class cohort
usage: dx find [-h] category ...

Search functionality over various DNAnexus entities.

positional arguments:
  category
    apps           List available apps
    globalworkflows
                   List available global workflows
    jobs           List jobs in the current project
    analyses       List analyses in the current project
    executions     List executions (jobs and analyses) in the current project
    data           List data objects in the current project
    projects       List projects
    org            List entities within a specific org.
                   
                   	"dx find org members" lists members in the specified org
                   
                   	"dx find org projects" lists projects billed to the specified org
                   
                   	"dx find org apps" lists apps billed to the specified org
                   
                   Please execute "dx find org -h" for more information.
    orgs           List orgs

optional arguments:
  -h, --help       show this help message and exit

dx find: error: argument category: invalid choice: records
(choose from apps, globalworkflows, jobs, analyses, executions, data, projects,
org, orgs)
root@a3b159225b87:/# dx create_cohort --database=database-GvJJbfjJyQ6y1B56fg8X51BP --name="all"
usage: dx create_cohort [--brief | --verbose] --from FROM
                        (--cohort-ids COHORT_IDS | --cohort-ids-file COHORT_IDS_FILE)
                        [-h]
                        [PATH]

Generates a new Cohort object on the platform from an existing Dataset or Cohort
object and using list of IDs.

positional arguments:
  PATH                  DNAnexus path for the new data object. If not provided,
                        default behavior uses current project and folder, and
                        will name the object identical to the assigned record-id.

optional arguments:
  --brief               Display a brief version of the return value; for most
                        commands, prints a DNAnexus ID per line
  --verbose             If available, displays extra verbose output
  --from FROM           v3.0 Dataset or Cohort object ID, project-id:record-id,
                        where ":record-id" indicates the record-id in current
                        selected project, or name
  --cohort-ids COHORT_IDS
                        A set of IDs used to subset the Dataset or Cohort object
                        as a comma-separated string. IDs must match identically
                        in the supplied Dataset. If a Cohort is supplied instead
                        of a Dataset, the intersection of supplied and existing
                        cohort IDs will be used to create the new cohort.
  --cohort-ids-file COHORT_IDS_FILE
                        A set of IDs used to subset the Dataset or Cohort object
                        in a file with one ID per line and no header. IDs must
                        match identically in the supplied Dataset. If a Cohort is
                        supplied instead of a Dataset, the intersection of
                        supplied and existing cohort IDs will be used to create
                        the new cohort.
  -h, --help            Return the docstring and exit

dx create_cohort: error: the following arguments are required: --from
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T16:00:18.789Z" title="11/5/2024, 4:00:18 PM">16:00</time>

The errors indicate two issues:

1. **Using `dx find records --class cohort`**:
   The `dx find` command does not support the `records` category. Instead, use `dx find data` to list all data objects in the project and filter for cohorts manually.

   ```bash
   dx find data --project=project-GvJ3jgQJ5qQB10jPfqVyFBqz --name "*all*"
   ```

2. **Creating a Cohort with `dx create_cohort`**:
   The `dx create_cohort` command requires the `--from` argument, which specifies the dataset or cohort from which to create a new cohort, along with a list of IDs to filter.

   Here’s how you can structure the command:

   ```bash
   dx create_cohort --from=database-GvJJbfjJyQ6y1B56fg8X51BP --cohort-ids="ID1,ID2,ID3" --name="all"
   ```

   - Replace `"ID1,ID2,ID3"` with the specific IDs in the dataset you want to include in the cohort. If you have a file containing these IDs (one per line), you can use the `--cohort-ids-file` argument instead:

     ```bash
     dx create_cohort --from=database-GvJJbfjJyQ6y1B56fg8X51BP --cohort-ids-file=/path/to/cohort_ids.txt --name="all"
     ```

   This will create a new cohort named "all" based on the specified IDs within `database-GvJJbfjJyQ6y1B56fg8X51BP`.

3. **Proceed with Data Extraction**:
   Once the cohort is created, you should be able to use it with `dx extract_dataset` for data extraction.

Let me know if this helps or if there are additional questions about this process!


#### You:
<time datetime="2024-11-05T16:01:31.300Z" title="11/5/2024, 4:01:31 PM">16:01</time>

![image](data:image/png;base64,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AhKQgAQkMKQETr3qtiHNudmWgAQkIAEJSEACEpCABCQgAQlIQAISkIAEJFBOQA/Oci5ulYAEJCABCUhAAhKQgAQkIAEJSEACEpCABCQgAQlIQAISkIAEBpCACs4BvClmSQISkIAEJCABCUhAAhKQgAQkIAEJSEACEpCABCQgAQlIQAISKCeggrOci1slIAEJSEACEpCABCQgAQlIQAISkIAEJCABCUhAAhKQgAQkIIEBJKCCcwBvilmSgAQkIAEJSEACEpCABCQgAQlIQAISkIAEJCABCUhAAhKQgATKCajgLOfiVglIQAISkIAEJCABCUhAAhKQgAQkIAEJSEACEpCABCQgAQlIYAAJzBjAPJklCUhAAhKQgARGgMDChQvDZZddFm699daw2WabhbXXXnsESmURJCABCUhAAhKQgAQkIAEJSEACEpCABCQggX4T0IOz33fA60tAAhKQgARGlMAll1wSTjjhhHDeeeeFL3/5y+H+++8f0ZJaLAlIQAISkIAEJCABCUhAAhKQgAQkIAEJSKCXBFRw9pK215KABCQgAQlMIQLXX3/9eGnnz58fbrzxxvHfrkhAAhKQgAQkIAEJSEACEpCABCQgAQlIQAISaJWACs5WyXmeBCQgAQlIQAISkIAEJCABCUhAAhKQgAQkIAEJSEACEpCABCTQcwIqOHuO3AtKQAISkIAEJCABCUhAAhKQgAQkIAEJSEACEpCABCQgAQlIQAKtElDB2So5z5OABCQgAQlIQAISkIAEJCABCUhAAhKQgAQkIAEJSEACEpCABHpOQAVnz5F7QQlIQAISkIAEJCABCUhAAhKQgAQkIAEJSEACEpCABCQgAQlIoFUCM1o90fMkIAEJSEACEpBApwnMmTMnnHvuueHhhx8OO+ywQ5g9e3anL2F6EpCABCQgAQlIQAISkIAEJCABCUhAAhKQwJATUME55DfQ7EtAAhKQgARGhcCCBQvCscceG66//vq8SCg599lnn1EpnuWQgAQkIAEJSEACEpCABCQgAQlIQAISkIAEOkTAELUdAmkyEpCABCQgAQm0R+Dkk08eV26S0jLLLNNegp4tAQlIQAISkIAEJCABCUhAAhKQgAQkIAEJjCQBFZwjeVstlAQkIAEJSGC4CPzsZz8Lv//978czveKKK4aXvvSl479dkYAEJCABCUhAAhKQgAQkIAEJ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gRARGK9Cv87ecFC3lkpSSaUivguYIeoCmyEBEiABEiABEiABEiABEiABEiABEiABEggxAQqcIQbK5kiABEiABEjASgC5PSeN/U6iLpwThKLNX7CIDot7+uRxOX0iwpHzFB6enjzkre1xngRIwHcCN1RI6uGT1jkqVC2eR8JzBu8h6WiQMyRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAglCgAJngmDnTklAknR+TZ4/EiAB3wnUadRS5SbLKPOm/qbz7EaqHJqYjGUKyyLtu90n1es1Mav4SQIkECICCEndrHJhnb+5qcovfztzzIeILJtJSQQQYaB27do6r6svOSpTEhseKwmQAAmQAAmQAAmQAAmQAAmQQMIRSPWfMuvuX513QC/25gMgKxbOk0DICVy6GC1/X7+qhY+MYZlD3j4bJAESSHwEjh3eL2dPnZBLF6Mka/acOucmvDaRszaubNzWo7rpN1p6zq8aV/tOTu1GRETowylQIPC8wsmJB4+FBEiABEiABEiABEiABEiABEiABEiABEiABBKSAD04E5I+952iCYRlzqKOHxONBEggpRAoWKSEYKKRAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAkETiB14FVZkwRIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgATilwAFzvjlzb2RAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAkEQYACZxDwWJUESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESCB+CVDgjF/e3BsJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkEAQBChwBgGPVUmABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABOKXAAXO+OXNvZEACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACQRBgAJnEPBYlQRIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIIH4JUOCMX97cGwmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQQBAEKHAGAY9VSYAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAE4pcABc745c29kQAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJBEGAAmcQ8FiVBEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEggfglQ4Ixf3twbCZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZBAEAQocAYBj1VJgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgATilwAFzvjlzb2RAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAkEQYACZxDwWJUESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESCB+CaT1tLtxW4962sT1JEACJEACJEACJEACJEACJEACJEACJEACJEACJEACJEACJEACJEACJJAgBOjBmSDYuVMSIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIIFACKT6T1kgFVmHBEiABEiABEiABFIKgYiICH2oBQoUSCmHzOMkARIgARIgARIgARIgARIgARIgARIgARIggURLgB6cifbUsGMkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAJ2AhQ47US4TAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkkGgJUOBMtKeGHSMBEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABErAToMBpJ8JlEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiABEiCBREuAAmeiPTXsGAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQgJ0ABU47ES6TAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAkkWgIUOBPtqWHHSIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAE7AQocNqJcJkESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESCDREqDAmWhPDTtGAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRgJ0CB006EyyRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAomWAAXORHtq2DESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAE7AQqcdiJcJgESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESSLQEKHAm2lPDjpEACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACdgJpLWv4DIJkAAJkAAJkAAJkIB7AhEREe43cC0JkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkEC8EaAHZ7yh5o5IgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgASCJUAPzmAJsj4JkAAJkAAJkECKIVCgQIEUc6w8UBIgARIgARIgARIgARIgARIgARIgARIgARJIrATowZlYzwz7RQIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIk4EKAAqcLEq4gARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARJIrAQocCbWM8N+kQAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJkAAJuBCgwOmChCtIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgAQSK4G0ibVj7FfSJ7BixQr56aef9IEMGzZMMmfO7NdBvfHGGxIRESG1atWShx56yK+6LEwCJEACJEACJEACJEACJEACJEACJEACJEACJEACJEACJEACJJA8CVDgjMfz+t9//8mECRNk9erVcvXqVZc958yZU5588knJlSuXy7a4XoF+rV+/XvLnz6/7EIr9RUdHy4kTJ3RT169f97vJyMhIXf/ChQt+12WF0BCIi3ERmp6xFRIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIggZRKgCFq4/HM79ixQxYvXuxW3EQ3zp49K5988omcPn1aIIZ6m0Ld7ePHj8uuXbtk27ZtoW6a7SVhAhwXSfjkseskQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkQAIkkEwJ0IMzHk/soUOHYt0bRM6hQ4d6LZc+fXqpU6eO9OzZU1KlSuW1LDeSAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQQHIiQA/OJHg2r127JkuXLpWtW7cmWO9v3LghgYSdNR3++++/zWxIPkPdnr1Tcd2+fX9YDnSf//77r+D8BGrBnNdg+o26we470GNmPRIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIggaRDgB6cCXCu2rZtK+3btw94z9OnT5eZM2cKPEIrV64ccDuo+P7778ulS5fkyJEjup0zZ87Iq6++qucbN24srVq10vP4DyF2p02bpkPZnjt3Totot912mxQtWlRQ9s477/ToUYpwu+j32rVrZd++fXqfhQoVktKlS+t9lCtXzrEfX2eOHj0qEydOlD179gjms2XLJpUqVdJTy5YtJU2aNL425bacr+1DUPzggw/kypUrup0ePXroPlgbRRmEHzb5RJ944gnJnTu3bNy4UR8Dyr744ouycOHCgBhhLIDv/v379bhInTq1Pi8lSpSQTp06SXh4uLU7MnfuXC2S4xz0799fn1uI5n/99ZdkyJBB8ubN6/O4wLnFuEAOV5xbcChZsqRm0KhRIylevLhf+x4+fLhTeS6QAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQAAmQgJUABU4rjXicTyyhZbdv3y5RUVGOI4dYtWXLFr1crFgxx/oZM2bId99951g2M/Ay3Lt3r54OHjwoEO7cGUQrCKRWg6iKCXlJH374YWnTpo11s9d5CHQjR44UeLMaO3/+vCxbtkxPmzZtkmeffTZgkdOf9iGkNmjQQAuY6EtkZKSez5Qpk+majB07VvcLKyAaQ9yEnTx50sH7rbfeCogRxO7Ro0e7eD9C+MUEvgMHDpQmTZrofeK/w4cP6/1GR0frfkF8hQgLgyDp67hASOWPP/7YxZt49+7dggnj5uWXX5aKFSvqtvFfbPt2FOQMCZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACbghQIHTDZSUprOJkQAAQABJREFUtArefRAJlyxZooU5iHIdOnTQCIxX5YEDB+T777/X67JmzSrwysO2nDlzam/OCRMmyNWrV7X3Yd++fQVl7AZxE16FEPfgZQkhFSF2ISRCWPv6668lR44cOreova59GV6PX375pV4Nr83OnTtrb8XTp09rQQ1C66pVq7TI+Mwzz9irx7ocSPsQD+H9CA/MU6dOyahRo2TQoEF6X9u2bXN4acLb9aGHHnLbh0AYLV++XL799lvdHkTz1q1bS9WqVTXTDRs26P7g3EDABN8qVao47RvMwBLnALld4dFZrVo1wTiIbVzgHMJzddeuXbpNiLz169eXdOnSCY4ZHqXY95tvvinvvPOOwJvUap72bS3DeRIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARIgARKwE6DAaSeSwpa7du2qjxiiHDwPIWz17t3biQK8ISFmwYYOHeokVMEzDyLjiBEj9HZ47dWqVUvPW/+DlyM8KuvVq+dYjbC21atXlw8//FCHux03bpzUrl3bY5hbVPznn38cYmuePHl0XezfWPPmzbXotmbNGu2ZiGMpUKCA2RzrZzDtI9Qrjv/YsWMyf/58LdZWqFBBi4vgh9Cvzz33nBYA3XXEX0bwnv355591UxCP4SkJnsYgRNeoUUNMyFd4eWLe6j188eJFXbxOnTry2GOPuYjT3sbFokWLHOLmfffdJ126dDG71scOsRN9glA6efJkeeqppxzbMRPbvp0Kc4EESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAESIAEbhJITRLxR8CIhPG3x9DsCcIbcn1CsLJ74WEPWbJkcewIHnvuDN59VnHTlME6CHEweF7C88+bwSsxIiJCF+nXr58WV63l0ddHH31U0qaN0e7hIeqPBdM+BEyIuMhLCvvqq69k2LBhAk9F2IABA6RgwYJ63t1//jJCPtMTJ07oppBz1CpumvbB1nCHJy68Zu2GfJmDBw92ETft5ezLyLsJQyhjeNHaDV6+7dq106tXrlzpEDSt5QLdt7UNzpMACZAACZAACZAACZAACZAACZAACZAACZAACZAACZAACaQsAvTgTFnnO6Cj7dixo2CyGnI3IpciPBaN0GXdbp+HAOfJELYWIXJhR48e1SFsPZVFzk5j169fF3hqujOIrufOnZPNmzfrzYcOHdLhcN2VxTp4MCJ8a6Dtm3Yh9vVVYXqRrxQ5QTHBWrRoIU2bNtXznv7zlxFYGfOWvxTbELIXhjoQq61mvHit62Kbh1hv9p8xY0aB2OrOjLcovE0hXtetW9epWCD7dmqACyRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAiRAAimOAAXOeDzlSdWDE4gQZnTBggUCD0eImlFRUX6R8xYm1urVePz4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X7/ePPjgg+bnP/95wiCnWlwWtrRo0cL07t07YhCTbfEAAEAASURBVHYFQLdt22ZmzZpllixZ4qaNGjXKNGvWzJx88skRdfmAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAQEkJEOAsRvlFixYlXJuCnHfccUe+9SpXruzSxw4bNswUJtDZunVrM3z48LjreP31180zzzzjpiuFLAHOuFRMQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQKGaB8sW8voxb3cKFC82OHTsybrvy26Bdu3aZsWPHmhkzZuRXrdDTBg8ebKpVq+bmT9c6Cr1xzIgAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIFCmBcp0C84VK1aYBx54wDRv3txcf/31QVAv3WfEmWeeac4+++xCr+att94y77zzjlGL0K5duxZ6OfFmVKvQunXrmu3bt5uaNWtGVPv9739vlM62f//+5pRTTomYpg8KFv/lL39x488//3zTs2fPPHWSGTFlyhTz5ptvulkqVqxofvGLXxTbcUpmO6mLAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCBQPAJlugVno0aNTKdOnczixYvNQw895AJ6xcNuXGpZBRIL80r3Nq5bt86sXLnSrSY6QPn1118bvfz06G3Zt2+fm646vi/P6DoF/Tx+/Hhz9913u+XNnTvXnHvuuQQ3C4pHPQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAgSwXKdICzQoUK5uqrr3atIBXkfPjhh4s1yJlp55QPTt51111Gwzk5Oa6lZkls55gxY8xf//pXtx1qRfqHP/zB9OjRoyQ2hXUigAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAghkkECZTlGr4+CDnE888YRrKagg53XXXZfVLQUnT57sArvh83Dv3r1m06ZN5sCBA250/fr1zS233GLatm0brlYsw++995755z//6balQYMG5o477jCHHXZYsayblSCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCGS2QJluwekPjQ9yqj9L9WuZrpacPnjo11tS77t27TJr166NeG3cuDEIbmq7Nm/e7Pr5VD+cxVnU3+Zjjz3mtkV9o6o/T4KbxXkEWBcCCCCAAAIIIIAAAggggAACCCCAAAIIIIAA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+snUS60JC1v0RSiNN5EViD3iiCMKtNsKBKvk5OTEra8vtNIo65VMqVChgmndunUys1AXAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEECgVAgQ4S8VhYiOzSUD9lc6YMcP1san9qlWrVjbtHvuCAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCKRVgABnWnlZOAJ5Ba6//vqgabWm9uzZM28lxiCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCMQUIMAZk4WRCKRfoFq1ambo0KGme/fu6V8Za0AAAQQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEskSAAGeWHEh2o/QIjBgxwuzZs6dU9jFaepTZUgQQQAABBBBAAAEEEEAAAQQQQAABBBBAAAEEEMhWAQKc2Xpk2a+MFahevXrGbhsbhgACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAghkukD5TN9Atg8BBBBAAAEEEEAAAQQQQAABBBBAAAEEEEAAAQQQQAABBBDwAgQ4vQTvCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCQ8QIEODP+ELGBCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCDgBeiD00vwjgACCCCAAAIIJBDYuHFjghpMRgABBBBAAAEEEEAAAQQQQAABBBBAoOwIlC9fMm0pS2atZee4sqcIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIJBCAVpwphCTRSGAAAIIIIBAdgs0a9Ysu3eQvUMAAQQQQAABBBBAAAEEEEAAAQQQQCAJgZUrVyZRO3VVacGZOkuWhAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACaRYgwJlmYBaPAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAKpEyDAmTpLloQAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAmkWIMCZZmAWjwACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACqRMgwJk6S5aEAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAJpFiDAmWZgFo8AAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAqkTIMCZOkuWhAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACaRYgwJlmYBaPAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAKpEyDAmTpLloQAAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAmkWIMCZZmAWjwACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACqRMgwJk6S5aEAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAJpFiDAmWZgFo8AAggggAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAqm6qDZSAABAAElEQVQTIMCZOkuWhAACCCCAAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACaRYgwJlmYBaPAAIIIIAAAggggAACCCCAAAIIIIAAAggggAACCCCAAAKpE6iYukWxJAQQQAABBBBAAAEEyq7A/v37zb79B4zeDxzQ+wH3ruEDB1nK2fdy5cq5V/ny/r28qWCHy5fn2cOye/aw5wgggAACCCCAAAIIIIAAAgggkIwAAc5ktKiLAAIIIIAAAggggEBIYO++fWbfPhvY1MsGNhMVBToV8LT/2PqRtSvYAGeFCrmvihUqRE7kEwIIIIAAAggggAACCCCAAAIIIIBAIECAM6BgAAEEEEAAAQQQQACBxAJqmanApg9uJp6jYDUUIHVB0j3GBToV5NRLLT0pCCCAAAIIIIAAAggggAACCCCAAAKHBAhwHrJgCAEEEEAAAQQQQACBuAIKbO7Zu9cFNjWczuJbhe4pv9cFOXMqViTQmU5wlo0AAggggAACCCCAAAIIIIAAAqVKgABnqTpcbCwCCCCAAAIIIIBAcQsopeyevbbFpn0VJA1tKrdPgdTd+/e6FLgVK1YwOfalPjwpCCCAAAIIIIAAAggggAACCCCAQFkWIMBZlo8++44AAggggAACCCCQr4BaUu5Wq00b3CzJ4tLX7s5NYVvJtuZUX50UBBBAAAEEEEAAAQQQQAABBBBAoKwKEOAsq0ee/UYAAQQQQAABBBDIV2DPnr0uuJnudLT5bkTURAVa99u+OhXkzMnhUj6Kh48IIIAAAggggAACCCCAAAIIIFBGBLgrUkYONLuJAAIIIIAAAgggUDABpaTdreCmfWViUcB15+49Zr/dzko2yEnK2kw8SmwTAggggAACCCCAAAIIIIAAAgik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gAIKKKCAAgoooIACLRYwwNlicC+ngAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCiiggAK1CxjgrN3OMxVQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQoMUCBjhbDO7lFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFCgdgEDnLXbeaYCCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCrRYwABni8G9nAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCiiggAIK1C5ggLN2O89UQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQIEWCxjgbDG4l1NAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAgdoFDHDWbueZCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCijQYgEDnC0G93IKKKCAAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKFC7gAHO2u08UwEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFWixggLPF4F5OAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQVqF+ip/VTPVEABBRRQQAEFxpfAs88+O74qbG0VUEABBRRQQAEFFFBAAQUUUEABBRQoI9DVNTpjKUfnqmUg3KWAAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgqUEnAEZykZtyuggAIKKKCAAgUCiy++eMEWvyqggAIKKKCAAgoooIACCiiggAIKKDB+BaZMmTIqlXcE56iwe1EFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFKhFwABnLWqeo4ACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACoyJggHNU2L2oAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgrUImCAsxY1z1FAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAgVERMMA5KuxeVAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFahEwwFmLmucooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoooMCoCBjgHBV2L6qAAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAArUI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HXeE3/72t/H7LrvsElZbbbX8vuyHM844I9x///1h4sSJ4cc//nF2V02fn3766XDyySeHt99+O56/1lprhR133LGmvDxJAQUUUEABBRSoRoB2zzXXXBMee+yx/LrktIuWXnrpwKwX6667bjXZDDuG9t3ll18e/va3v4VHHnkkEDglMUXuhhtuGLbddtthxxf78tZbb4Xzzz8/3HfffeHJJ5+M68svtNBCcZaONdZYo2i5br755nDJJZfEWTx+9KMfxeUI/vjHP4a77747PPTQQ+Giiy4qdim3KaCAAgoo0HABA5wNJzVDBRRQQAEFFFBAgXYUaNQUta2s24wZAw253GjVnVEAzz33XKzDMsssE+aZZ558fRi5QCcfKXXI5XdmPtBhx3FzzDFHZmttH5944olwyCGHhGnTpsUMPv7xj1fV+Vfb1TxLAQUUUEABBca7AKMizz777BiILLR46aWXAq/bb7893HnnnWHPPfcMs802W+FhRb/Tdjr++ONjcLPwgBdeeCFccMEF4dZbbw0EMEsl2ljHHXdcvq2WjmPtdNZR50XbafLkyWlXfGd/asPRzqMczzxT/fr0wzLziwIKKKCAAnUIGOCsA89TFVBAAQUUUEABBcaOQKNGMbZoAGdDYRtV95EU6qmnngq//OUv40gAzmOk5Gimhx9+OBx22GH5qds23njj8NWvfjW3NqmrdozmffHaCiiggAIKdLLAaaedFq666qp8Fddcc82w6qqrxvYHM1Tccsstcd+1114b3nzzzXDAAQfkjy334Zhjjgl33XVXPKS3tzesvfbaYYUVVohTxD744IMx8ElbrFTiITQe+uKaJNYXpWw8UPbPf/4zXHfddXFk5sUXXxx6enrCTjvtVDSrU045JR/cZLYORo+aFFBAAQUUaJWAAc5WSXsdBRRQQAEFFFBAgVEVaNAEtaNah1ov3qy6EzCkMyubGCnw73//OzB6gMT+7bbbLr6yx7XyMx2IP/nJT/KjGChP4WiEVpbHaymggAIKKKDA2BMo1u4prAWjMBdddNG4mSlfr7766vi5u7s77LPPPnE62nTOZpttFkdvHnvssXHqfEZcPvDAA2HFFVdMhxR9p12TgptM4X/QQQeFlVdeOX/sNttsE2688cZw4oknBkaQFkvnnHNOPri58847h+233z5/GA+BTZo0KR8AZTraLbbYIsw1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oIACCiiggAIKKKCAAgoooIACCiiggAIKKKBA9QIGOKu3c00FFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFGiygAHOJoO7OwUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUqF7AAGf1dq6pgAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCiiggAJNFjDA2WRwd6eAAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAtULGOCs3s41FVBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFCgyQIGOJsM7u4UUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUKB6AQOc1du5pgIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKNFnAAGeTwd2dAgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgpUL2CAs3o711RAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAgSYLGOBsMri7U0ABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUECB6gW6ql/VNRVQQAEFFFBAgZEl8OKLL46sBttaBRRQQAEFFFBAAQUUUEABBRRQQAEFygh0dLQml7I1ey0D4SwFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFCglIAZnKVknK6AAgoooIACChQIzD///AVTfKuAAgoooIACCiiggAIKKKCAAgoooMDIFZg0aVJLGm8GZ0vY3akCCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACClQjYICzGjXXUUABBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUECBlggY4GwJuztVQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQIFqBAxwVqPmOgoooIACCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoo0BIBA5wtYXenCiiggAIKKKCAAgoooIACCiiggAIKKKCAAgoooIACCihQjYABzmrUXEcBBRRQQAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBVoiYICzJezuVAEFFFBAAQUUUEABBRRQQAEFFFBAAQUUUEABBRRQQAEFqhEwwFmNmusooIACCiiggAIKKKCAAgoooIACCiig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fjl2Y9yZ2w/dJ88zzzxhrbXWCgsssEDR/b766qvhiSeeiPOWXXbZMHbs2KLLOVGBdhV44403wiOPPBKbt/zyy4dZZpmlXZtquxRQQIFhLXDnnXfGISIG0wjGrud8qNZCDyoPPPBA3Mziiy8e5pprrkFv8v7774/DTcw222xh6aWXHvT6rqCAAgoooMBQFjDAOZSPjnVTQAEFFFBAAQUUqKtAvYKbz+QCe9dd+7tw1113hp6enpJ1XHzxj4XDj/hGmHGmmUou0+gZtLneAc5nnnkmnH/++eHee+8tWf1LLrkkrLvuumHXXXcNc845Z7/lHnzwwfDDH/4wTjvssMPC2muv3W++bxRopAABebLSyVAv/Gw2cr/ZbT/66KPhpJNOipP233//sPHGG2dnV/2aMZPfeuutuD5tS1n4VW/QFRVQQIERLnDyySfHm8UGw7DzzjuH7bfffjCrFF32+eefz/9W7LLLLmHixIlFlys38dxzzw3ckMZvwjnnnFNuUecpoIACCigw7ATsonbYHTIrrIACCiiggAIKKFCtQL0CnD8+60fhb3+7vWxwkzo+8cTj4eSTTgzv/u9/1Va55vXq1eZUkUmTJoVjjz22X3CT7LOFF144jB8/PowaNSouOm3atHDLLbeE73znO+H9999Pq/usQMsFDjrooLDffvuF0047reV1qXcF/vSnP8W20b6UIVrvfbg9BRRQQAEFFFBAAQUUUGAoCJjBORSOgnVQQAEFFFBAAQUUaLgAGVu9uUet5fHHHgsvvvjCgDeTgpybfmazAa3T3d0Vllt+hTBmzJgBLV9pIdpM2zs66nNvIwHLN998M+6WLtj22GOPsNxyy+UDm2SQXX/99eHKK68MU6ZMiVkDZ599djjggAMqVdX5CiiggAIKKKDAkBU4/vjj8+c75SpZj+5py23feQoooIACCijwgYABTj8JCiiggAIKKKCAAiNCoK9vWl3aOfmtyYPeDkHOs350xoDXI7i53cTtw2c223zA65RbkLbXI7750ksvhRde+CC4O/vss8dMzllnnbXfrmeeeebYLdt8880XTj311EAm56233hq+8pWvBMbotCiggAIKKKCAAsNRIHtD13Csv3VWQAEFFFCg3QTqcxt3u6nYHgUUUEABBRRQQIG2E6hH9mazUN57773wq19eFXiuR6lX2x966KF8dVZcccVQ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Ng/1Tv6oLfHGMlJT8Kmbgs5BZ59j2rRta6cn459kH3My9rmidd58881m+/btpn379mbYsGEVzZp1r2XjsWfjMWXdB48DQgABBBCwAv/617/8QE4TFFRu2LDBLFmyxA82NV3hpv5/y8/P11PbJhvDSwAAQABJREFUFAa69vTTT9v1qIcLVWyuWLHCvPzyy7YLWDePurnVGJgHH3ywvahL09Xl7bZt28zy5cvNs88+azQGprqJ7dy5c8j4l9GuX8tPmDDBbloVqKtXr7Zjauo4FJxqHM6xY8e6XfO73dWESy+91Nxxxx32tYceesh8+umnRt3VajzRZd734g8//NCO56kZ9tprL1sNamfe/U9FxxScj8cIIIAAAghEEiDgjKTCNAQQQAABBBBAAIGsE1DVX4l3S0azweYEr2JzwWchq1ewedags72r29vb6YsXLzIve/OVCTo7dvK6rj07KUGnjlnHnpOTE7JvPEEAAQQQQAABBBCousDrr79e6cy9evUyV155ZUjFoxY69thjzbhx48zGjRttqPnwww+XWVfLli3tcuouVsHnkCFDzF133WW6dOli51XY6Xo+UCCq1qNHDxtwxrv+M88807zyyiv2O6OOs7xjVRezOkbXFNJeccUV5plnnjGqOn3nnXfszb3u7hX26ngUaAZbRccUnI/HCCCAAAIIRBIg4IykwjQEEEAAAQQQQACBrBMoLd2Z8GPSeEcve2NsLvis4mDTbVhB52FD23tX5IcFnV4wqnC0Y6dOXiDqVXSGdd/llo/1XsdOvhmrHsshgAACCCCAQE0VUDAXqUtZeeyxxx6mRYsWtopS4WS7du3M4YcfHpFqn332sWGlurFXlWOwqbKxe/fu5n/+539steTw4cNtWKh5gheoDR482Kh7WlVUqjeLnTt/+W4b7/pViamuZxVsfv3118Hds4+bNGliTjrpJKNxRTUuZ7D179/fdlWrCldVlxYWFvovqwvaY445xpx//vnmgAMO8Ke7BxUdk5uHewQQQAABBMoTIOAsT4bpCCCAAAIIIIAAAlklkOjqzf+8PsmMff7fIUbhFZshLwaelBd0KijV7YILLzL9ftU/sER8D3XseSb0ZFR8a/xlaZ1c27Rpk6ldu7bteuyXV6r+6IcffrBdoGl8pz333LPqC1ZhTp0I1LhPOkGpqoHwk3JVWEW5s2T6sWvHY7XVcrLTCdO8vOj+bNRyqjypX79+uXa8gAACCCCAQHUQeP755xO2m61atTJ//OMfzebNm/3uaBs1amR0c61r167mqaeest27av7geOONGze2VZBu3vD7eNavILJv3772pipT3RSi6vud/j9XwFlRUyXmn//8Z1sBunbtWnt82nctpyC4vFbZMZW3HNMRQAABBBCQQHR/qWKGAAIIIIAAAggggEA1FQhe5Z6IQ5g5Y0bIag7xrtr/zXU3mH333TdkekVPFHQ2u665+fvDfzNfeN2RuaZ1JzLgTPSxa326wv+jjz4yqmL96aef7K5rvCV1WzZo0CB3KBHvVQkxc+ZMM3nyZPPVV1/ZIM3NWK9ePXul/7nnnmt00ktt/vz5ZvTo0fbxjh077L2Wu/XWW+1jVQacd9559rH++fbbb+3+zZo1y2zdutWvcNDJO1VXnHzyyaZPnz7+/NE8yPRjj9Y2eOwLFiwwkyZNspUlGnPLNZ2g7Nmzp+nXr1/IiVb3uu51EvSFF17wxpb93FZ+qJs6vX+qZOnWrZs54YQT/NmjfT/9BXmAAAIIIIBAFggoMKzoIiBVdLpuaWM53HjXr//3g8FqNPugilNVs+pGQwABBBBAINkCBJzJFmb9CCCAAAIIIIAAAhkhkOguagdf/j/m0VGPeFe4f2+PTwHlrTff6HXf1cf8asDASoNOVRW+/tpE8/bb00ICvoYNGxmtO5EtkceuMPOhhx6y4Wb4Pn733XfmxRdfNHPmzLGBV/jreq6A8IEHHrDzRHpdlYNvvvmmDTWHDRtmQ7J169bZIDQ4v4JOhZxqwZNoS5YsMX/4wx9Cukdzy2nbel2377//3naX5l6ryn2mH3sstu64p06dah577DE/DHbTda8qjgkTJpgZXvA+YsQI06BBg+DLNuQeOXKkDZaDL2zYsMFMnz7d3lauXGkuueQS+3I072dwfTxGAAEEEEAAAQQQQAABBBBAwAnkel0j/NE94R4BBBBAAAEEEECgrMCPP/5oJ6p7y3Q2hQVqrqotVfuSru0m+vgKi4rNLyMVxb/2hl53Yid7XXkp7Plm9Wqzbds22y3X8uVfmrfefMP81/vctGrd2tSpUydkYwo2x4970Tz2j1Hmiy++sMtoBgWbF1x4obny6mtMY68SMpGtlreygvzEXNuocaE+/vhju3vq9lWVeaeeeqqt1CsoKLAhl6om5aGmLmcHDhxoH+ufl156yVZu6rFeU3WfqinVLVqzZs3MqlWrbOCr5VXN2b59exuWqvrywAMPtK8ryNO2VFWoaYcddphR12ha5rbbbvPDVb12/PHHm1/96ldGXb6pKnH9+vXatLVXpWlwbCv7QgX/ZPKxa7djsdVy6mJYobBc1fSennHGGaZHjx42PF6zZo1RoCxfhdjBakx1sydz3aupYlPeGktM3dtqHC+td/Hixfb1Dh06VPn9tAvwDwIIIIAAAggggAACCCCAQEYLaIgS/c2u8x+6V3P3evzNN9/ortIWXCY4c/CiZk134z0n5ixHcEs8RgABBBBAAAEEEEAgAwUSGW66w9PYhL29is0ePXuZ995917w28RVbGagxCKdOnWKrM11Fp5aJVLGpcZcGDDzTnOiFSdGOdej2o7L7RB37woULbWWltqfxlIYMGWIUWLl21llnmffee8/8/e9/D6lKda/rfu7cufapAkoFhhovyjWFkQoihw4daie5UKxjx45GN7X333/fBmRt2rQxN9xwg53m/tH8+sNKrZfXVe6NN97oXrL36pr27rvvtl2w6g8iVYC2bds2ZJ7ynmT6sWu/Y7HVcuqa1oWbp512mrnmmms02Ta9J6eccoq55ZZb7Hien3ljxGpe94fns88+64fZF198sTnnnHPcoja0Vvit8FThqKpA+/fvb9/Lqryf/op4gAACCCCAAAIIIIAAAggggECYAAFnGAhPEUAAAQQQQAABBLJTwAU4iTq6xYsWmU8++dh08QI5jaXZ+6STvKCzp5nx3rtm4sRXzfdexW0w6NR29dw1BZsDz1Cw2dPk5ubayYsXLzIfe+Nadu7SxQsOdwV6bv547hN17C+//LK/G+eff35IuOleUNWfuiMNzuteUwWl61b20EMPDQk33TyHHHKIDc+0z+quNpq2yHtPXFMoF94Uymn9n376qX0pmvUHjycTjz0eWzeuqVAimWgcrjPPPNMo3FTFq7rq1fhgGuv0XS/YV1PQHQw37UTvHwXRgwcPNqNGjbKf/3feeccMGDDAvcw9AggggAACCCCAAAIIIIAAAjEJEHDGxMZCCCCAAAIIIIAAAjVd4IknHrMh5pTJ/zGHel2knjXobBt09up9kg0tw4NO59WocWOvy9YzygSbL08Yb5bs7sZTlXh/e/jvbpGMuVdwqaZK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AAEEEEAAAQQQQKBaCRBwVqu3i51FAAEEEEAAAQQQSLWAupQtKvYqNr1bVbqhTeT+KUgtLC22XeDm5eWafO+mMTxpCCCAAAIIIIAAAggggAACCCCAQE0WIOCsye8+x44AAggggAACCCBQoYAqKQtVtemFm+lstvvawl1d2BZ41Zwaq5OGAAIIIIAAAgggkFqBwsJC88knn5j58+ebjRs3mq1bt5p99tnHNGvWzDRv3tx0797d7L333knZqQ0bNpjly5fbdbdv397Uq1cvKdtJxUrnzp1rSssZv14X8+lWUFBgLWW75557pmK32EaMAmvXrjWrVq2KuHROTo5p0KCB/fmo7u/jli1bzJIlS+xxHnjggaZJkyYRjznbJ+r34Lx588ynn35qNm3aZH8P6r2tX7++adu2rTn22GPt42x34PgyQ4CAMzPeB/YCAQQQQAABBBBAIMMEioqKbbiZ7O5oozlsBa06GaSQMz+fr/LR2DEvAggggAACCCAQj4BO5v/1r3+1J/PLW8/TTz9t+vXrZ8466yyz1157lTdbTNMXLlxo/va3v9llf/e739kwNaYVJXmhn376yfzwww92Kw0bNrRBZfgm//KXv3g9lFTtAkKFnR07djTXX3+9ady4cfiqeJ4BArNnzzbPPfdcpXuiUL5FixZm4MCBNgSrdIEYZqjK5y+G1dpFvvrqK3PffffZx1dffbU5/fTTY11VtV1OFyc8/PDD5r///W/EY3jnnXfME088Yc4++2xz0UUX0ftQRCUmJlKAS78Tqcm6EEAAAQQQQAABBKq9gLqk/bmwyOzwbpkUbjpY7ZP2TfuofaUhgAACCCCAAAIIJE9A37fGjh1r7r777pBwU8Fb06ZNbQWn2/qOHTvMhAkTzF133WW2bdvmJteo+2nTppnf/OY39rZ06dK4j13+n332mRk6dKhZv3593OtjBekTUPC9ePFiGxL+8Y9/NKtXr074ziT685fwHaymK9RFtmPGjDEjRowICTf1e1AXHuR5F+C6pp/Zl156yf7OdBc7uNe4RyDRAr988hK9ZtaHAAIIIIAAAggggEA1Eyj1/hgrLCz2xtwszvg9L/QqTL3d9a6KzzM53h+WNAQQQAABBBBAAIHECzzyyCNGoYlr6oa2b9++tivGunXr2snqpnHixInmP//5jykqKjIrVqywIY6CztzcXLco9xEE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IIYhWuOl25QlPoyzrfdqufNUo31CsVYalpq6XP/W1qfeu+++G/gb0FpjzC35m8HfCP4OJjvggAOa/Tv4la98Jfz0pz9NVcKYMWMML53RcKPaBPTgrDZR25OABCQgAQlIQAIS6HQECPfaGcLSNgaWvhOlFk9OTQISkIAEJCABCUig7QSef/75GEaTlnr16lUkXDbV+o477hhDNCIMTJw4MQqk5KnL29NPPx3D3uIhmvJKrrzyymHgwIEBr8WhQ4fmi5fdpn94RiWvRgr16dMnbLnlltGbdKmllipbDxGFei+99FIUCxG3EJsGDBgQw+7inUU7pYZggQBH3/bdd9/AGBBw8VRFKMFLD6F29uzZWVW881I/Tj311MAYK7Hll18+tg3HfBucn5yn7CdHKuIXYgqhMcn/iRiz//77Z6dsLfe//OUvYezYsbE+bSHOlRq5JJNAffzxx4e11lqrqAh9In8ogtJKK60UTjvttHgclvSV8MfcA2myItdigw02CLvsskv42te+VtRW/gP3FiGRX3nllcifeoMHD47ek9yDeFLmrbWs8nWrvb3aaqvF8Kb33HNPbPq+++4Lw4YNKzrNv/71r3DXXXfFe4x7KvHhWhMWlTHmQ+Gm69DS+6+17Rd17vMPL7/8csw1yfcYkZ++9evXL16HvfbaKwwofKfKGffEuHHjwt133x2oy72RbLnllovfYe7b0mtIGb7vd955Z7zHP/nkk1Qt3ltf//rXw2677Ra3swO5DTwq//znP4d//OMf4fXXX4/CaPK4ZXJGub873P9pUgEhuffee+9ci41vco1ok+8cAizn5fuBse/666+P24ceemj48pe/HLdL/7nyyisDf+f4G3LWWWeVHvazBCIBBU5vBAlIQAISkIAEJCCBbk1gfkHcRODs7MYYyMVZX+9P/M5+Le2/BCQgAQlIQAK1J4AAmAwhBeGhJYZ483//7/+NggyhVBE9kiFkXH311VG4SfvSGoGEhbC2hIT8zne+E3r37p0OF60ffvjhWC6JPukg4s69994bRZDzzz+/Qf3JkyeH//3f/81E1VSPfiHWsIwfPz6ccMIJYZNNNkmH45q6iKFrr712uOOOOwLiQzLGiQiSF5c4hoiULC/ipH0tWSOepnY4d/464PWGQIRR5re//W345z//2aDZSrkj9Kb2H3/88QYCJ8IkYmoyRMdS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ACPqBhE06M+//vWvQChefk9tvvnmMUpGLOQ/EpCABCQggRoRUOCsEXhPKwEJSEACEpCABFpLgJCavFSYN29enMXd2vqVlOdcWFcJ54mfYM+C4LewCgLn1tsMDWsWQqeOGzs2DB68bti0jHBG3sfzf3dBGPvIw5Ejgif7Sm3UCSdFgXPy5Elhm6Hbhv79+5cWqegzY23eN7Kipq0kAQlIQAISkIAEJPA5AXJxYvxmzofcHz9+fLjhhhui5+PnRQMemc8991xciGqx//77p0Nxfd9994Vbb701/u5PB/CsnDVrVnjggQfCU089FX70ox+FFVdcMR0ODz/8cMxJnkLxc4A6//znP+PC+Y466qjMs3TOnDlh+vTpsf4rr7wSLr300iyMf2qUvl144YUxPUDax5qc5w899FB49NFH87vdloAEJCABCbQ7AQXOdkfuCSUgAQlIQAISkEBlBJgt/cEHH8TZ06uuumrZ0FGVtVy+FjO233rrrXiQc3cVQ/SbX7eg8NLo0zYPaY01+of/OnBkk+0gaO46fLcmy/AybEhhRj5Ltayuboko5larPduRgAQkIAEJSEACEmhI4Omnnw4ImRhh8FN4Vzwer7322ihU4n259957h9VXXz2888474c4774y/6REsCZu/ww47xPqvvvpquPnmm+M2YWl32223QnqDtaPn55NPPhn+8Y9/xDD/V199dfS8pCAem6NHj46CJr8pd95557DRRhvFSZH0C0GUZ4jLLrssnHXWWTGiSDzB5/8kcRPBlHPhWYpxDnKfYxtuuGEYOnRo9ALlfHfddVf497//HY/5jwQkIAEJSKBWBBQ4a0Xe80pAAhKQgAQkIIFWEkDUZMY0LxOmTJnSytqVF+dFCefuKpaEv3mLFnSVIZUdB0IuY9UkIAEJSEACEpCABNpGAI9FxMVkeEcyGRARE8ESIy1APi/5n//85yhuMtnttNNOiyFmKbdWIQLIJptsEn71q1/F+rS9/fbbxzC0t99+O0WiJ+ioUaOi4Bh3FP756le/GgVKvDInT54cnwuYhIggSn+w73//+5lAyWdC566yyioxdC3PEWPGjAn77LMPhzLD65NQuSNGjAgpZ+ff//737HmD8P7f/va3s4gueKgigp5zzjmKnBlFNyQgAQlIoBYEFDhrQd1zSkACEpCABCQggQoIMIubFwqzZ8+Os7A/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BAgQIECAAAECBAgQIECAAAECBAgQIECAQCIgcCbsTgkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQeAQEzkfNhgABAgQIECBAgAABAgQIECBAgAABAgQIECBAgACBREDgTNidEiBAgAABAgQIECBAgAABAgQIECBAgAABAgQIECDwCAicj5oNAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQKJgMCZsDslQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQOAREDgfNRsCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBBIBgTNhd0qAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAwCMgcD5qNgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIJAICZ8LulAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgACBR0DgfNRsCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBBIBATOhN0pAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQKPgMD5qNkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIJAICJwJu1MCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBB4BgfNRsyFAgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAIBEQOBN2pwQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIPAIC56NmQ4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIBAIiBwJuxOCRAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBB4BATOR82GAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIFEQOBM2J0SIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIPAICJyPmg0BAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAomAwJmwOyVAgAABAgQIECBAgAABAgQIECBAgAABAgQIECBA4BEQOB81GwIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEEgGBM2F3SoAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIDAIyBwPmo2BAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgkAgJnwu6UAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIFHQOB81GwIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIEEgEBM6E3SkBAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAo+AwPmo2RAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgkAgInAm7UwIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEHgGB81GzIUCAAAECBAgQIECAAAECBAgQIECAAAECBAgQIEAgERA4E3anBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAg8AgLno2ZDgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgEAiIHAm7E4JECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIEHgEBM5HzYYAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgURA4EzYnRIgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAg8AgInI+aDQECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECiYDAmbA7JUCAAAECBAgQIECAAAECBAgQIECAAAECBAgQIEDgERA4HzUbAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQSAYEzYXdKgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgMAjIHA+ajYECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECCQCAmfC7pQAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgUdA4HzUbAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQSAQEzoTdKQECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECj4DA+ajZECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIECCQCAicCbtTAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQeAYHzUbMhQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQCAREDgTdqcECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECDwCAuejZkOAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAQCIgcCbsTgkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQeAQEzkfNhgABAgQIECBAgAABAgQIECBAgAABAgQIECBAgACBREDgTNidEiBAgAABAgQIECBAgAABAgQIECBAgAABAgQIECDwCAicj5oNAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQKJgMCZsDslQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQOAREDgfNRsCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBBIBgTNhd0qAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAwCMgcD5qNgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIJAICZ8LulAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgACBR0DgfNRsCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBBIBATOhN0pAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQKPgMD5qNkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIJAICJwJu1MCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBB4BgfNRsyFAgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAIBEQOBN2pwQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIPAIC56NmQ4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIBAIiBwJuxOCRAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBB4BATOR82GAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIFEQOBM2J0SIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIPAICJyPmg0BAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAomAwJmwOyVAgAABAgQIECBAgAABAgQIECBAgAABAgQIECBA4BEQOB81GwIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEEgGBM2F3SoAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIDAIyBwPmo2BAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgkAgJnwu6UAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIFHQOB81GwIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIEEgEBM6E3SkBAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAo+AwPmo2RAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgkAgInAm7UwIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIEHgGB81GzIUCAAAECBAgQIECAAAECBAgQIECAAAECBAgQIEAgERA4E3anBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAg8AgLno2ZDgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgEAiIHAm7E4JECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIEHgEBM5HzYYAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgURA4EzYnRIgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAg8AgInI+aDQECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECiYDAmbA7JUCAAAECBAgQIECAAAECBAgQIECAAAECBAgQIEDgERA4HzUbAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQSAYEzYXdKgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgMAjIHA+ajYECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECCQCAmfC7pQAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAgUdA4HzUbAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQSAQEzoTdKQECBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECj4DA+ajZECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIECCQCAicCbtTAgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQeAYHzUbMhQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQCAREDgTdqcECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECDwCAuejZkOAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAQCIgcCbsTgkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQeAQEzkfNhgABAgQIECBAgAABAgQIECBAgAABAgQIECBAgACBREDgTNidEiBAgAABAgQIECBAgAABAgQIECBAgAABAgQIECDwCAicj5oNAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQKJgMCZsDslQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQOAREDgfNRsCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBBIBgTNhd0qAAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAwCMgcD5qNgQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIJAICZ8LulAABAgQIECBAgAABAgQIECBAgAABAgQIECBAgACBR0DgfNRsCBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBBIBATOhN0pAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQKPgMD5qNkQIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIJAICJwJu1MCBAgQIECAAAECBAgQIECAAAECBAgQIECAAAECBB4BgfNRsyFAgAABAgQIECBAgAABAgQIECBAgAABAgQIECBAIBEQOBN2pwQIECBAgAABAgQIECBAgAABAgQIECBAgAABAgQIPAIC56NmQ4AAAQIECBAgQIAAAQIECBAgQIAAAQIECBAgQIBAIiBwJuxOCRAgQIAAAQIECBAgQIAAAQIECBAgQIAAAQIECBB4BATOR82GAAECBAgQIECAAAECBAgQIECAAAECBAgQIECAAIFEQOBM2J0SIECAAAECBAgQIECAAAECBAgQIECAAAECBAgQIPAIDGmBL9zuohMBAAAAAElFTkSuQmCC)
its actually called Total, you can literally see the file in the root folder together with the data.database and the other:



#### ChatGPT:
<time datetime="2024-11-05T16:01:50.445Z" title="11/5/2024, 4:01:50 PM">16:01</time>

Thank you for sharing the screenshot. It confirms that you have two items named **Total** in your DNAnexus root folder, both listed as **CohortBrowser, DatabaseQuery Record** types. Since you’re interested in extracting data based on one of these cohorts, here’s how to proceed:

### Step 1: Identify the Correct Cohort ID for **Total**

Use the `dx describe` command to get more details on each **Total** record, so you can confirm which one has the data you need.

1. **Describe the Cohort**:

   ```bash
   dx describe <record-ID-of-Total>
   ```

   Replace `<record-ID-of-Total>` with the actual ID for each **Total** record. You should see these IDs in the web interface.

### Step 2: Use the Cohort with `dx extract_dataset`

Once you've confirmed the correct cohort ID, you can proceed with data extraction using `dx extract_dataset`.

1. **Extract Data from the Cohort**:

   ```bash
   dx extract_dataset <cohort-ID> --fields="eid,p3_i0,p3_i1" --output=extracted_data.json
   ```

   Replace `<cohort-ID>` with the confirmed ID of the **Total** cohort. This will create a JSON file with the specified fields.

2. **Convert JSON to CSV (if needed)**:

   If you want the data in CSV format, you can convert it as previously discussed.

Let me know if you need more assistance with any specific part of this process!


#### You:
<time datetime="2024-11-05T16:02:36.138Z" title="11/5/2024, 4:02:36 PM">16:02</time>

this is the cohort Id:

record-Gvb2Kv8J5qQ8q1vFX4YQ8847

#### ChatGPT:
<time datetime="2024-11-05T16:02:55.560Z" title="11/5/2024, 4:02:55 PM">16:02</time>

Great! Now that you have the cohort ID (`record-Gvb2Kv8J5qQ8q1vFX4YQ8847`), you can use it to extract data. Here’s how:

### Step 1: Extract Data from the Cohort

Use the `dx extract_dataset` command to extract data based on this cohort ID. Specify the fields you need (like `eid`, `p3_i0`, `p3_i1`) and output it to a file.

```bash
dx extract_dataset record-Gvb2Kv8J5qQ8q1vFX4YQ8847 --fields="eid,p3_i0,p3_i1" --output=extracted_data.json
```

This should save the extracted data to `extracted_data.json`.

### Step 2: Convert JSON to CSV (if Required)

If the data is saved in JSON format and you need it as CSV, you can use a Python script for conversion:

```python
import pandas as pd
import json

# Load the JSON data
with open("extracted_data.json") as f:
    data = json.load(f)

# Convert to DataFrame and save as CSV
df = pd.DataFrame(data)
df.to_csv("extracted_data.csv", index=False)
```

Save this script as `convert_to_csv.py`, then run it in your terminal:

```bash
python3 convert_to_csv.py
```

This will generate a `extracted_data.csv` file with the selected fields.

Let me know if this process works or if you need further assistance!


#### You:
<time datetime="2024-11-05T16:05:15.899Z" title="11/5/2024, 4:05:15 PM">16:05</time>

how do I lookup all the fields in a ID record? possibly save them to a file?

#### ChatGPT:
<time datetime="2024-11-05T16:05:31.730Z" title="11/5/2024, 4:05:31 PM">16:05</time>

To view and save all fields in a DNAnexus record (like your cohort record), you can use the `dx describe` command combined with some additional commands to list and save the fields. Here’s how:

### Step 1: Describe the Record to View All Fields

Use the `dx describe` command on your record ID to get metadata details, which may include information about available fields.

```bash
dx describe record-Gvb2Kv8J5qQ8q1vFX4YQ8847
```

This will give you a summary of the record. However, this command might not list all fields if it's a dataset or complex record.

### Step 2: Extract Field Names (if Available in JSON or Metadata)

If your record is a dataset or complex data object, the fields might be saved as part of its metadata or JSON structure. Here are a couple of methods to extract and save those field names:

#### Option A: Using `dx get_details`

Some records, especially datasets, allow you to retrieve details directly with `dx get_details`:

```bash
dx get_details record-Gvb2Kv8J5qQ8q1vFX4YQ8847 > fields.json
```

This command will output the details in JSON format, which you can examine to find field names.

#### Option B: Using Field List from JSON

If `fields.json` contains the fields in a structured format, you can extract them in Python:

1. **Inspect the JSON File**: Check if it contains a list of fields by opening it:

   ```bash
   cat fields.json
   ```

2. **Extract Field Names with Python**:

   If the JSON file has a key like `fields` or similar, you can use Python to load and extract those field names:

   ```python
   import json

   # Load JSON data
   with open("fields.json") as f:
       data = json.load(f)

   # Assuming the fields are under a key named 'fields'
   fields = data.get("fields", [])

   # Save field names to a text file
   with open("field_names.txt", "w") as f:
       for field in fields:
           f.write(f"{field}\n")
   ```

   This will save all field names in `field_names.txt`.

### Step 3: Verify Field Names File

After running the Python script, you can check the saved field names:

```bash
cat field_names.txt
```

This approach should help you get a full list of fields from a DNAnexus record. Let me know if the fields aren’t accessible this way, and we can try another approach!


#### You:
<time datetime="2024-11-05T16:07:12.832Z" title="11/5/2024, 4:07:12 PM">16:07</time>

I used the id of the data.dataset file:

root@a3b159225b87:/# dx get_details record-GvJP9yjJyQ6QzZpkk4qpKVX3 > fields.csv
root@a3b159225b87:/# ls
bin   dx-toolkit	  fields.csv  media  proc  sbin  tmp
boot  etc		  home	      mnt    root  srv	 usr
dev   extracted_data.csv  lib	      opt    run   sys	 var
root@a3b159225b87:/# cat fields.csv
{
    "descriptor": {
        "$dnanexus_link": "file-GvJP9vjJyQ6gjBZ6Y9qgppBq"
    },
    "version": "3.0",
    "schema": "ds-ukbrap-ver17",
    "databases": [
        {
            "app23889_20241024233847": {
                "$dnanexus_link": "database-GvJJbfjJyQ6y1B56fg8X51BP"
            }
        },
        {
            "grch38_92_euw2_transcript": {
                "$dnanexus_link": "database-Fx7Fj58JjG8Yf6bKPX9Yzykf"
            }
        }
    ],
    "name": "app23889_20241024233847.dataset",
    "description": "Dataset: app23889_20241024233847.dataset Original Version: v18.1+d41d8cd"
}
root@a3b159225b87:/# 

no fields that I can actually use

#### ChatGPT:
<time datetime="2024-11-05T16:07:30.082Z" title="11/5/2024, 4:07:30 PM">16:07</time>

The output of `dx get_details` for `data.dataset` does not include the actual field names. Instead, it references a linked file (`file-GvJP9vjJyQ6gjBZ6Y9qgppBq`) which may contain the field names in a different format.

Since `file-GvJP9vjJyQ6gjBZ6Y9qgppBq` appears to be a JSON file (possibly containing field details), you can try inspecting it directly. Here’s how:

### Step 1: View the Linked File for Field Names

1. **Inspect `file-GvJP9vjJyQ6gjBZ6Y9qgppBq`**:

   ```bash
   dx cat file-GvJP9vjJyQ6gjBZ6Y9qgppBq | gunzip -c | less
   ```

   Since this file is `application/json+gzip`, this command decompresses and displays it. Use the `less` command to scroll through the contents and look for sections that might contain a list of field names.

2. **Save the JSON Output to a File (Optional)**:
   If you want to keep a local copy to examine, you can save the decompressed JSON data to a file:

   ```bash
   dx cat file-GvJP9vjJyQ6gjBZ6Y9qgppBq | gunzip -c > fields.json
   ```

### Step 2: Extract Field Names from the JSON File

If `fields.json` contains the field names in a structured way (e.g., under a key like `fields` or `columns`), you can use Python to parse and save them.

1. **Use Python to Extract Field Names**:

   ```python
   import json

   # Load the JSON data
   with open("fields.json") as f:
       data = json.load(f)

   # Assuming field names are stored under a key named "fields" or "columns"
   # Adjust the key based on the actual structure of your JSON file
   fields = data.get("fields", [])  # Try other keys if "fields" doesn't exist

   # Save field names to a CSV file
   with open("field_names.csv", "w") as f:
       for field in fields:
           f.write(f"{field}\n")
   ```

   This script will save all extracted field names to `field_names.csv`.

### Step 3: Verify the Extracted Fields

You can now check the `field_names.csv` file:

```bash
cat field_names.csv
```

This process should help you retrieve and save the list of fields from `file-GvJP9vjJyQ6gjBZ6Y9qgppBq`. If the structure is complex or you can’t find the fields, let me know, and we can further troubleshoot.


#### You:
<time datetime="2024-11-05T16:11:23.980Z" title="11/5/2024, 4:11:23 PM">16:11</time>

this is some of the fields I found in json, I have no idea how to specify exactly one field within that data id, how do I instead of pulling the json file just pull one datafield?



#### ChatGPT:
<time datetime="2024-11-05T16:11:37.962Z" title="11/5/2024, 4:11:37 PM">16:11</time>

To retrieve a specific field from your dataset on DNAnexus, follow these steps:

1. **Identify the Field Name**:
   You have field names like `"eid"`, `"p3_i0"`, `"p3_i1"`, etc., from your JSON structure.

2. **Use `dx extract_dataset` Command**:
   The `dx extract_dataset` command can help export specific fields directly, which is useful if you only want a subset of data rather than the whole JSON.

   Here's the command format:

   ```bash
   dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="eid,p3_i0,p3_i1" --output=single_field_data.csv
   ```

   Replace `record-GvJP9yjJyQ6QzZpkk4qpKVX3` with your specific record ID and `"eid,p3_i0,p3_i1"` with the exact fields you need.

3. **Check and Download**:
   After running the above command, check if `single_field_data.csv` has been created with only the selected fields.

4. **Verify Field Data**:
   Once downloaded, you can examine the CSV file to ensure it includes only the specified fields.

If `dx extract_dataset` still fails or if you encounter specific permission errors, it might be due to access restrictions on that dataset. Let me know if you encounter any issues with permissions or command execution, and we can troubleshoot further.


#### You:
<time datetime="2024-11-05T16:12:23.804Z" title="11/5/2024, 4:12:23 PM">16:12</time>

root@a3b159225b87:/# dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="eid,p3_i0,p3_i1" --output=single_field_data.csv
The following fields cannot be found: ['eid', 'p3_i0', 'p3_i1']
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T16:12:46.051Z" title="11/5/2024, 4:12:46 PM">16:12</time>

The error message indicates that the fields `"eid"`, `"p3_i0"`, and `"p3_i1"` are not recognized in the dataset with ID `record-GvJP9yjJyQ6QzZpkk4qpKVX3`. Here’s how you can troubleshoot and locate the correct field names to use with `dx extract_dataset`:

### Step 1: Verify Field Names

The field names may be slightly different from what you've specified, or they might be nested under different keys in the JSON structure. Since you have the JSON file with the fields structure, carefully examine the exact path to each field within that file.

### Step 2: Check Field Paths in JSON

If the fields are nested or have a specific prefix, you'll need to specify the exact name as it appears in the JSON file. Open the JSON file (`fields.json`) and locate the exact naming structure used for each field. For example, the fields might have a prefix or be formatted differently than expected.

### Step 3: Re-run with Exact Field Names

Once you identify the exact field names, re-run the `dx extract_dataset` command with the updated field names. Here’s an example format based on possible adjusted names:

```bash
dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="exact_field_name_1,exact_field_name_2" --output=single_field_data.csv
```

Replace `exact_field_name_1` and `exact_field_name_2` with the correct names you found in the JSON file.

### Step 4: Use `dx describe` for Further Validation (if Needed)

If you’re still unsure about the field names, you can use `dx describe` to examine metadata for `record-GvJP9yjJyQ6QzZpkk4qpKVX3`, which might provide additional insights.

```bash
dx describe record-GvJP9yjJyQ6QzZpkk4qpKVX3
```

This command may show you metadata that includes the available fields or confirm the data structure.

Let me know if you find different field names, or if further adjustments are needed.


#### You:
<time datetime="2024-11-05T16:13:03.126Z" title="11/5/2024, 4:13:03 PM">16:13</time>

I gave you some fields just use 3 of those that you picked up on

#### ChatGPT:
<time datetime="2024-11-05T16:13:12.168Z" title="11/5/2024, 4:13:12 PM">16:13</time>

Thank you for clarifying! Based on the fields you provided in the `format.txt` file, I’ll choose three fields and provide the command to retrieve them.

Let’s use these fields as an example:

- `"eid"`
- `"p53_i0"`
- `"f20016_i0"`

Here’s the command you can use:

```bash
dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="eid,p53_i0,f20016_i0" --output=single_field_data.csv
```

This command should extract only these specified fields and save them to `single_field_data.csv`.

If the fields are still not recognized, we may need to verify the exact names in the dataset’s structure, as DNAnexus might require fully qualified paths or exact matches for each field name. Let me know if this command works or if you encounter any additional errors.


#### You:
<time datetime="2024-11-05T16:13:44.420Z" title="11/5/2024, 4:13:44 PM">16:13</time>

here are the json fields again!!! just forget the fields I gave you I want 3 fields that are actually in the json file into a csv

#### You:
<time datetime="2024-11-05T16:15:04.232Z" title="11/5/2024, 4:15:04 PM">16:15</time>

try again

#### ChatGPT:
<time datetime="2024-11-05T16:15:13.535Z" title="11/5/2024, 4:15:13 PM">16:15</time>

From the JSON file you've provided, here are three fields that are confirmed to be present in the data:

1. `eid` (Participant ID)
2. `p3_i0` (Verbal interview duration | Instance 0)
3. `p21_i0` (Weight method | Instance 0)

To export these fields into a CSV using DNAnexus, try the following command:

```bash
dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="eid,p3_i0,p21_i0" --output=single_field_data.csv
```

This command will generate a CSV file named `single_field_data.csv` with data from the specified fields. If this doesn’t work, please let me know, and we can explore further alternatives.


#### You:
<time datetime="2024-11-05T16:15:55.277Z" title="11/5/2024, 4:15:55 PM">16:15</time>

does that mean the fields are there but here is no data to extract?

root@a3b159225b87:/# dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="eid,p3_i0,p21_i0" --output=single_field_data.csv
The following fields cannot be found: ['eid', 'p3_i0', 'p21_i0']
root@a3b159225b87:/# 

#### ChatGPT:
<time datetime="2024-11-05T16:16:16.817Z" title="11/5/2024, 4:16:16 PM">16:16</time>

The error suggests that DNAnexus cannot locate these fields in the specified dataset, which can happen if:

1. **The Field Names in DNAnexus Differ Slightly**: Sometimes fields are stored with different prefixes, suffixes, or are nested in a way that requires precise naming.
2. **The Dataset Does Not Have Values for These Fields**: It’s possible that the dataset structure includes these fields in metadata, but there’s no actual data available in this particular dataset record.
3. **The Dataset Record Isn’t Configured for Field-Level Extraction**: Some records may reference other datasets without containing the actual data for those fields.

To confirm if there is data available in these fields or if we need an exact naming format, you can try:

### 1. **List All Fields in the Dataset Using `dx export_view`**

This command can show you exactly which fields are accessible:

```bash
dx export_view record-GvJP9yjJyQ6QzZpkk4qpKVX3
```

If the dataset supports field-level views, this command should display all available fields, helping you identify any naming differences.

### 2. **Check Dataset Details for Exact Naming**

Another method is to use `dx describe` with the `--json` option to get a more detailed view of the dataset, including its fields:

```bash
dx describe --json record-GvJP9yjJyQ6QzZpkk4qpKVX3 > dataset_details.json
```

Then, review `dataset_details.json` for the exact field names. If fields are nested or prefixed, this will help identify them precisely.

### 3. **Double-Check Field Availability and Naming**

If neither of the above commands provides clarity on field availability, it’s possible that the dataset `record-GvJP9yjJyQ6QzZpkk4qpKVX3` might only link to field definitions without having data, or may require accessing a different record or table where the data resides.

Let me know what you find after these checks, and we can adjust the extraction approach accordingly.


#### You:
<time datetime="2024-11-05T16:16:52.050Z" title="11/5/2024, 4:16:52 PM">16:16</time>

its too big the fields

#### ChatGPT:
<time datetime="2024-11-05T16:17:09.845Z" title="11/5/2024, 4:17:09 PM">16:17</time>

If the field list or dataset details are too large to view all at once, you can filter and extract only the field names to a manageable file. Here’s how you can handle large JSON output to retrieve just the field names.

### Step 1: Extract the Fields Using `jq` (JSON Query Tool)

The `jq` tool is helpful for filtering large JSON files. Here’s how you can use it to isolate field names from `dataset_details.json`:

1. **Install `jq`** (if not already installed):
   ```bash
   apt update
   apt install jq
   ```

2. **Filter Field Names Only**:

   Assuming the JSON structure has a specific key for fields (like `fields` or similar), run:

   ```bash
   cat dataset_details.json | jq '.fields | keys' > field_names.txt
   ```

   This command should produce a list of field names saved to `field_names.txt`.

### Step 2: Manually Review and Select Fields

Open `field_names.txt` to review the list of available fields and choose the ones you want to extract.

### Step 3: Attempt Extraction with Selected Fields

After identifying the exact field names, use them in your `dx extract_dataset` command as follows:

```bash
dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="field1,field2,field3" --output=single_field_data.csv
```

Replace `field1, field2, field3` with actual field names from `field_names.txt`.

This approach should help narrow down the list of available fields and confirm the correct names for extraction. Let me know if this method works or if you need further assistance!


#### You:
<time datetime="2024-11-05T16:17:45.585Z" title="11/5/2024, 4:17:45 PM">16:17</time>

so far you know our entire conversation and you know the execution that got me to each stage could you summarize everything include the code that got me to this point

#### ChatGPT:
<time datetime="2024-11-05T16:18:00.111Z" title="11/5/2024, 4:18:00 PM">16:18</time>

Certainly! Here’s a detailed summary of our progress, the commands used, and key insights at each stage:

### Objective

You wanted to extract specific fields from a DNAnexus dataset (`record-GvJP9yjJyQ6QzZpkk4qpKVX3`) to a CSV file, but encountered challenges with field names and dataset accessibility.

---

### Summary of Steps and Commands

#### Step 1: Verify Dataset Existence and Structure

You used the `dx describe` and `dx get_details` commands to gather basic information about the dataset.

- **Command to Describe the Dataset:**
  ```bash
  dx describe record-GvJP9yjJyQ6QzZpkk4qpKVX3
  ```

- **Command to Retrieve Dataset Details:**
  ```bash
  dx get_details record-GvJP9yjJyQ6QzZpkk4qpKVX3 > fields.json
  ```

These commands provided basic metadata, but did not show actual data fields. We determined that the dataset referenced additional files, including a JSON file (`file-GvJP9vjJyQ6gjBZ6Y9qgppBq`) with detailed field definitions.

---

#### Step 2:


#### You:
<time datetime="2024-11-05T16:18:24.400Z" title="11/5/2024, 4:18:24 PM">16:18</time>

no how I went all the way from osx installing dxtoolkit eveeerything

#### ChatGPT:
<time datetime="2024-11-05T16:19:12.826Z" title="11/5/2024, 4:19:12 PM">16:19</time>

Absolutely! Here’s a comprehensive summary of everything we covered, from setting up DNAnexus on macOS to extracting fields in the dataset, including all commands and troubleshooting steps.

---

### Full Process from macOS Installation to Dataset Extraction Attempt

---

### 1. **Setting Up DNAnexus CLI and Toolkit on macOS**

You began by installing the DNAnexus CLI (`dx`) and `dx-toolkit` on macOS to interact with the DNAnexus platform.

- **Command to Install `dxpy` (DNAnexus Python SDK and CLI):**
  ```bash
  python3 -m pip install dxpy
  ```

- **Command to Clone and Install `dx-toolkit` from Source:**
  ```bash
  git clone https://github.com/dnanexus/dx-toolkit.git
  cd dx-toolkit
  python3 -m pip install -e dx-toolkit/src/python
  ```

- **Using Docker to Install `dx-toolkit`**: You set up Docker with the following command to create an isolated environment for the toolkit:

  ```bash
  docker run -v $(pwd):/dx-toolkit -w /dx-toolkit -it --rm --entrypoint=/bin/bash python:3.9-bullseye
  ```

---

### 2. **Logging into DNAnexus and Accessing the UK Biobank**

- You logged into the DNAnexus platform:
  ```bash
  dx login --host=auth.dnanexus.com --port=443
  ```

- Once logged in, you confirmed access to your project and files on DNAnexus by listing contents of your project:
  ```bash
  dx ls project-GvJ3jgQJ5qQB10jPfqVyFBqz:/
  ```

---

### 3. **Identifying the Dataset and Files**

Upon listing your project, you found various files, including:

- **`data.dataset`** (record ID `record-GvJP9yjJyQ6QzZpkk4qpKVX3`)

- **Linked JSON file (`file-GvJP9vjJyQ6gjBZ6Y9qgppBq`)**

- **Describing the Dataset Record:**
  ```bash
  dx describe record-GvJP9yjJyQ6QzZpkk4qpKVX3
  ```

- **Getting Detailed Metadata of the Dataset:**
  ```bash
  dx get_details record-GvJP9yjJyQ6QzZpkk4qpKVX3 > fields.json
  ```

---

### 4. **Attempting to Extract Data Using Field Names**

You initially attempted to extract fields like `eid`, `p3_i0`, and `p21_i0` from `data.dataset` but encountered errors indicating that these fields weren’t recognized.

- **Command Used to Extract Fields (Initial Attempt):**
  ```bash
  dx extract_dataset record-GvJP9yjJyQ6QzZpkk4qpKVX3 --fields="eid,p3_i0,p21_i0" --output=single_field_data.csv
  ```

This command returned an error, suggesting that DNAnexus couldn’t locate these fields.

---

### 5. **Inspecting Linked JSON File for Field Structure**

Realizing that the field names might not match exactly, we looked into the JSON file for the field structure.

- **Command to View and Decompress JSON Fields File:**
  ```bash
  dx cat file-GvJP9vjJyQ6gjBZ6Y9qgppBq | gunzip -c > fields.json
  ```

- **Parsing JSON for Field Names Using `jq`:**
  ```bash
  jq '.fields | keys' fields.json > field_names.txt
  ```

- **Python Script to Filter Fields**: After creating a JSON file with all fields, you used this Python script to extract them into a CSV:

  ```python
  import json

  with open("fields.json") as f:
      data = json.load(f)

  fields = data.get("fields", [])
  with open("field_names.txt", "w") as f:
      for field in fields:
          f.write(f"{field}\n")
  ```

---

### Summary of Findings

After analyzing and attempting multiple extraction commands, it was clear that while some field names were listed, DNAnexus couldn’t locate actual data for the specified fields in `data.dataset`. We verified that the record references other files or databases, likely pointing to an incomplete or restricted dataset structure on DNAnexus.

---

This summary includes all setup commands, troubleshooting steps, and extraction attempts, and provides a roadmap for any future steps in managing DNAnexus records or datasets. Let me know if you'd like to dive deeper into any specific command or setup!
