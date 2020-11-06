# WSO2 API Cloud Documentation

| Build Status |
|:------------- 
| [![Build Status](https://wso2.org/jenkins/view/Dashboard/job/docs/job/docs-cloud/badge/icon)](https://wso2.org/jenkins/view/Dashboard/job/docs/job/docs-cloud/) |

---

This is the WSO2 API Cloud documentation repository.

This repository is open and we welcome your contributions! 

## Contribute to WSO2 API Cloud documentation

Before you start contributing, read the following contribution guidelines to understand how you can start contributing to our documentation.

1. Accept the Contributor License Agreement (CLA)

    You need to Accept the Contributor License Agreement (CLA) when prompted via a GitHub email notification when you send your first Pull Request (PR). Subsequent PRs will not require CLA acceptance.

    If the CLA changes for some (unlikely) reason, you will be presented with the new CLA text when you send your first PR after the change.

2. Fork this repository, make your changes, and send in a pull request (PR). 

Check the issue tracker for open issues that interest you. We look forward to receiving your contributions.

## Run the project locally

### Step 1 - Install Python

If you are using MacOS, you probably already have a version of Python installed on your machine. You can verify this by running the following command:

```shell
$ python --version
Python 2.7.2
```

If your version of Python is Python 2.x.x, you also need to install Python3. This is because the PDF plugin only supports Python3. Follow the instructions in [this guide](https://docs.python-guide.org/starting/install3/osx/) to install Python3 properly.

Once you are done, you will have two versions of Python on your machine; a version of python2 and a version of python3.

### Step 2 - Install Pip
>
> **INFO**
>
> If pip is not already installed on your machine, download `get-pip.py` to install pip for the first time. Then run the following command to install it:
> ```shell
> $ python get-pip.py
> ```
>

Pip is most likely installed by default. However, you may need to upgrade pip to the latest version:

```shell
$ pip install --upgrade pip
```

### Step 3 - Install the pip packages

1. Navigate to the `<language-folder>/` folder.

    ```shell
    $ cd docs-cloud/en
    ```

2. Install the required pip packages.

    This will install MkDocs and the required theme, extensions, and plugins.

    - If you are using Python2, use the following command:

      ```shell
      $ pip install -r requirements.txt
      ```

    - If you are using Python3, use the following command:

      ```shell
      $ pip3 install -r requirements.txt
      ```

### Step 4 - Run MkDocs

Follow the steps below to clone the API Cloud documentation GitHub repository and run the site on your local server.

1. Fork the GitHub repository: `https://github.com/wso2/docs-cloud`
2. Navigate to the place where you want to clone the repo.

    Git clone the forked repository.

    ```shell
    $ git clone https://github.com/[git-username]/docs-cloud.git
    ```

3. Navigate to the folder containing the repo that you cloned in step 4.1 on a terminal window.

    For example:

    ```shell
    $ cd docs-cloud/<Language-folder>/
    ```

    ```shell
    $ cd docs-cloud/en/
    ```

4. Run the following command to start the server and view the site on your local server.

    ```shell
    $ mkdocs serve
    ```

    > **NOTE:**
    >
    > If you are making changes and want to see them on the fly, run the following command to start the server and view the site on your local server.
    > 1. Navigate to the `mkdocs.yml` file.
    > 2. Change the following configuration to `false` as shown below: 
    >     ```
    >     #Breaks build if there's a warning
    >     strict: false
    >     ```
    > 3. Run the following command to start the server and to make the server load only the changed items and display the changes faster. 
    >
    >    `mkdocs serve --dirtyreload`
  

> **NOTE:**
>
> If you are running the `mkdocs serve --dirtyreload` command to run the MkDocs server, make sure to change the configuration in the `mkdocs.yml` file as follows before sending a pull request.
>
> `strict: true` 

## License

Licenses this source under the Apache License, Version 2.0 ([LICENSE](LICENSE)), You may not use this file except in compliance with the License.

