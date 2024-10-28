## Version Control with Git in Azure Repos

**Requirements**

- Set up an Azure DevOps organization: If you don’t already have an Azure DevOps organization that you can use for this lab, create one by following the instructions available at [Create an organization or project collection](https://docs.microsoft.com/azure/devops/organizations/accounts/create-organization).
- If you don’t have Git 2.47.0 or later installed yet, start a web browser, navigate to the [Git for Windows download page](https://gitforwindows.org/) download it, and install it.
- If you don’t have Visual Studio Code installed yet, from the web browser window, navigate to the [Visual Studio Code download page](https://code.visualstudio.com/), download it, and install it.
- If you don’t have Visual Studio C# extension installed yet, in the web browser window, navigate to the [C# extension installation page](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp) and install it.

**Instructions**

1. **Configure Git and Visual Studio Code** (skip if done)
    You must install and configure Git and Visual Studio Code, including configuring the Git credential helper to securely store the Git credentials used to communicate with Azure DevOps. If you have already implemented these prerequisites, you can proceed directly to the next step.
    1. On the lab computer, open **Visual Studio Code**.
    2. In the Visual Studio Code interface, from the main menu, select **Terminal | New Terminal** to open the **TERMINAL** pane.
    3. Make sure that the current Terminal is running **PowerShell** by checking if the drop-down list at the top right corner of the TERMINAL pane shows `1: powershell`.
    4. In the TERMINAL pane, run the following command below to configure the credential helper:
        ``bash``
        git config --global credential.helper wincred
    5. In the TERMINAL pane, run the following commands to configure a user name and email for Git commits (replace the placeholders in braces with your preferred user name and email eliminating the < and > symbols):
        ``bash``
        git config --global user.name "<Seu Nome>"
        git config --global user.email <seu-email@example.com> 

2. **Create and configure the team project** (skip if done) 
    Create an Azure DevOps Project to be used to synchronize and version project code in CI/CD pipelines.
    1.  In a browser window open your Azure DevOps organization. Click on New Project. Give your project a `name` and choose your `Work item process` as you prefer. Click on **Create**.
    ![Create new project](docs/imgs/create-project.png)

3. **Import your Git Repository**
    Export the Git Repository that holds the code that will be verified.
    1. In a browser window open your Azure DevOps organization and the previously created project. Click on **Repos>Files , Import**. On the `Import a Git Repository` window, paste the Git Repo URL <https://github.com/{username}/{repository}.git> and click on `Import`.
    ![Import Repo](docs/imgs/import-repo.png)

4. **Set main branch as default branch**

    1. Go to **Repos>Branches**.
    2. Hover on the `main` branch then click the ellipsis on the right of the column.
    3. Click on **Set as default branch**.

**Following this steps you can use Git for version control in Azure Repos.**