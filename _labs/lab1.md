# Lab 1 - GitHub Advanced Security Feature Introduction

Welcome! In this lab, you will be introduced to GitHub Advanced Security (GHAS) and its features. You will use the Juice Shop sample repository to enable the GHAS features, manage alerts, and learn how GitHub Advanced Security can keep vulnerabilities out of your code in the first place.

## Exercise 1: Create the repository

We need to provision our working copy of the repository in order to begin the labs!

1. Navigate to URL: [https://github.com/joshjohanning-org/juice-shop-ghas-workshop](https://github.com/joshjohanning-org/juice-shop-ghas-workshop) TODO: update URL with universe repo
2. Click on the **Use this template ▾** button.
3. Make sure you have the **githubuniverseworkshops** organization selected.
4. Name the repository **YOUR_USERNAME-juice-shop-ghas-workshop**.
5. ❗️❗️ Make sure to check the box to **Include all branches**. The other branches are required in order to complete the workshop. ❗️❗️
6. Click the green **Create repository** button to create the repository

Once the repository is created, you will be automatically redirected to it.  Continue on to Exercise 2.

## Exercise 2: Enabling the security settings

In this exercise, you will be guided through the process of enabling the remaining GHAS features. Then you will be shown how to use the features to secure your code.

### Exercise 2.1: Enable Dependabot

1. We first want to turn on the security settings for the repository. Navigate to the **Settings** tab (the icon of the gear) in the repo.
2. Click on the  **Code security & analysis** section.
3. Although Dependabot isn't part of the GitHub Advanced Security product suite, it is still an important tool to discuss from an overall security posture. To enable Dependabot, we first have to enable the Dependency Graph. If it's not already enabled, enable the **Dependency Graph**. This allows Dependabot to ingest your package manifest files.
4. Click the **Enable** button next to the **Dependabot alerts** setting. This feature will create alerts for vulnerable dependencies found in your repository.
5. Optionally, enable Dependabot security updates. This will automatically create pull requests to update your vulnerable dependencies (if there is a non-vulnerable version to upgrade to). Note: there is a [maximum number of pull requests that this feature will create (10)](https://docs.github.com/en/enterprise-cloud@latest/code-security/dependabot/working-with-dependabot/troubleshooting-dependabot-errors#dependabot-cannot-open-any-more-pull-requests).

### Exercise 2.2: Enable Code Scanning

1. Next, let's enable **Code Scanning with CodeQL**. These settings are also under the **Code security & analysis** settings page.
2. Underneath the GitHub Advanced Security | Code Scanning heading, click the **Set up** button in the **CodeQL analysis** row.
3. There are two options: **Default** and **Advanced**. For this lab, we will use the **Default** setup which creates a workflow behind the scenes (i.e. you will not see it committed to the repo). You can use the Advanced option to manage your code scanning workflow as a GitHub Actions workflow YAML file committed to the repo.
4. Select the **Default** option, review the settings. By default, we will scan the JavaScript code, use the default CodeQL queries (for highest precision), and scan the default branch on push, pull request, and on a weekly schedule.
5. Click the **Enable CodeQL** button to save the settings and enable Code Scanning.
6. Ensure that **Copilot Autofix** is enabled (in the Code Scanning --> Tools section).
7. Optionally, configure the **Check runs failure threshold** - by default, a pull request will be blocked if there are any high or higher security alerts.

> [!NOTE]  
> You don't need a Copilot license in order to use the Copilot features with GitHub Advanced Security. However, Copilot can certainly be helpful in resolving issues in your IDE by using Copilot chat to explain the vulnerability and how to fix it.

### Exercise 2.3: Enable Secret Scanning

1. If it's not already enabled, click on the **Enable** button to enable Secret Scanning.
2. Check the box to **Use AI detection to find additional secrets (beta)**. This feature uses AI to find secrets/passwords that may be in your code that don't correspond to a known provider pattern.
3. Click the **Enable** button next to the **Validity checks** setting. This feature checks if the secret is still valid for [specific partners](https://docs.github.com/en/enterprise-cloud@latest/code-security/secret-scanning/introduction/supported-secret-scanning-patterns#high-confidence-patterns), such as AWS and, of course, GitHub. As an example, you can use this feature to check if a GitHub personal access token found in the repo is still valid and needs to be revoked.
4. Click the **Enable** button next to the **Non-provider patterns** setting. This scans for patterns that don't correspond to partners but still have a common syntax, such as a MySQL or MongoDB connection string.
5. Click the **Enable** button next to the "Push protection" setting. This feature will block pushes that contain high-precision secrets. You can use this [chart](https://docs.github.com/en/enterprise-cloud@latest/code-security/secret-scanning/introduction/supported-secret-scanning-patterns#supported-secrets) to determine which types of secrets would be blocked with secret scanning push protection enabled.
6. Optionally, configure **Who can bypass push protection for secret scanning**. To not potentially interrupt developers' workflows, by default anyone with write access to the repository can manually bypass a blocked push that contains secrets (administrators will be notified of this, and it is also captured in the audit logs). You can change this to only allow select users/teams (or no one) to bypass secret scanning push protection.
7. Note that you can define your own **Custom patterns** from this page to scan for secrets that don't correspond to a known provider pattern.

## Summary

Congrats! You have successfully enabled all of the security settings on your repository. In the next lab, we will review the alerts that have been created and how to manage them.
