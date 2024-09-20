# Lab 2 - Reviewing and Managing Security Alerts

Now that we have all of the security feature enabled, let's review the security alerts that have been created and how to manage them.

## Exercise 1: Reviewing Dependabot alerts

1. Click the **Security** tab in the repo. This is where you can see and manage all of the security alerts for the repo.
2. Click **Dependabot** under the **Vulnerability alerts** heading.
3. You should see a number of Dependabot alerts with various severities. Click on one of the alerts to see more information about it.
4. When reviewing a Dependabot alert, you can see the following information (see if you can locate this information in the alert you opened):
   - The severity of the alert
   - The package name and version that is vulnerable
   - The severity of the vulnerability
   - The CVE number
   - The affected versions of the package
   - The fixed version (if there is one - sometimes there isn't a non-vulnerable version to upgrade to)
   - The dependency path (what file contains the vulnerable dependency)
   - The alert description
   - The alert recommendation (to upgrade or use a different package)
   - The alert timeline (for example, it should show that Dependabot just recently opened the alert. Once you close an alert, it will show who and when closed it here too).
5. You can manually close an alert by clicking on the **Dismiss alert** button in the upper right hand corner. It's not recommended to close alerts manually, but there may be times where this is helpful (for example, the code that contains the alert is not used).
    - If you resolve an alert by upgrading to a non-vulnerable version, Dependabot will automatically close the alert!
6. If there is a non-vulnerable package version to update to, you will see a **Create Dependabot security update** button to queue Dependabot to attempt to create a pull request automatically to upgrade the vulnerable dependency. With this feature, assuming your build and tests pass, you can merge the pull request to close the alert.
    - TODO: Do we want to have them actually do this? or do you think showing/telling them about it is good. enough. Right now I think showing/telling is good enough. We can always add steps to have them do it if we need to lengthen the labs
7. Go **back** to the prior page and let's take a look at the list of Dependabot alerts again.
8. We can filter by **Package**, **Ecosystem**, **Manifest**, and **Severity**. For example, sometimes upgrading just one package can resolve multiple security alerts, so this can be a great way to prioritize fixes.
9. If you put your cursor in the search box (should have `is:open` by default), there are additional filter options. Some of the common filter options are **scope** (runtime or development) and **has** (for example, `has:patch`).
10. Update the search query to `is:open has:patch`. This will filter out all of the alerts that don't have a patch available and only show alerts where there is a non-vulnerable version to upgrade to.

## Exercise 2: Reviewing Code Scanning alerts

1. Under the **Security** tab in the repo, click on **Code scanning** to review the code scanning alerts.
2. We should have a number of alerts. If you don't see any alerts yet, skip ahead to the next exercise and come back to this one. More than likely, the code scanning workflow hasn't finished yet (it takes between 2-5 minutes to run).
3. If there are code scanning alerts, spend a few moments reviewing them. We can **filter/sort** by severity, tool, language, and a few other options, just like with Dependabot alerts.
4. A common search/filter to use is using **Autofilter** to filter out the alerts with a **test** tag (code scanning violations found in test files). This can help you focus on the alerts that are more likely to be real vulnerabilities.
5. To use the autofilter filter, paste this into the search box: `is:open branch:main autofilter:true` (or type/select it by hand).
6. Scroll down and let's click on one of the SQL injection alerts. These can be found by searching for the title **Database query built from user-controlled sources**.
7. After clicking into one of the alerts, we should notice a few things:
   - The severity of the alert
   - The CWE(s) of the alert with a hyperlink
   - The tool that found the alert (CodeQL)
   - The alert title
   - The alert description
   - More information on the alert, such as a recommendation and example of the vulnerability (and often additional resources to reference)
   - The alert file path, line number, and code snippet
   - The affected branch
8. CodeQL works by scanning the sources and sinks; as an example, the source is the user input and the sink is the database query. Click on the **Show paths** link to review the vulnerability from the source to the sink. This can help you understand the vulnerability and track it throughout the application to better understand how to fix it.
9. Oftentimes, there will be a lot of information to help understand the vulnerability and how to fix it. There should be a **Show more** expandable section that will show more information about the type of vulnerability you're working with.
10. In the upper right-hand corner, there is a **Generate fix** button to use Copilot to generate a fix for the vulnerability. Click it! This is a great way to learn how to fix the vulnerability and to see how to fix it in the context of your code.
11. It will take a little time to generate a suggestion.
12. If you're happy with the suggestion, click the **Create PR with fix** button. This will create a pull request with the fix for the vulnerability. In a real world example, assuming your build and tests pass, you would merge the PR.
13. The nice thing with code scanning alerts (just like Dependabot alerts) is that once you merge the code that resolves an alert, the alert will be automatically closed. This is because the alert is no longer present in the code. After merging the code into the default branch, a code scan will run and once it finishes, the alert will be closed. You can test this by merging the pull request we just created!
14. If you did merge the pull request, check back on the list of code scanning alerts under the **Security** tab in the repo. Once the code scan finishes running, you should see one (1) **Closed** alert listed.
    - #TODO: May have to flesh this out more (see comment: https://github.com/joshjohanning-org/universe2024-ghas-workshop/pull/1/files#r1760207693)

> [!NOTE]  
> You don't need a Copilot license in order to use the Copilot features with GitHub Advanced Security. However, Copilot can certainly be helpful in resolving issues in your IDE and Copilot chat can explain the vulnerability and how to fix it.

## Exercise 3: Reviewing Secret Scanning alerts

1. Under the **Security** tab in the repo, click on the **Secret scanning** --> **high confidence** option. This will show all of the high confidence secret scanning alerts.
2. You should see a number of alerts. For example, there should be a **GitHub Personal Access token alert**. Click it.
3. This alert shows where in the code the secret was discovered (if there were multiple locations, it would list them all).
4. If a secret is found in the code, we would want to revoke manually in the designated service. It's recommended to revoke the secret instead of rewriting history because the secret was exposed and you don't know who may have seen it. If you rewrite history, the secret will still be valid and could be used by an attacker. Also, rewriting history modifies commit hashes and can make traceability more difficult.
5. You can click on **Verify secret**. It will say it's not currently valid on github.com, but that doesn't mean it doesn't come from another GitHub instance (such as GitHub Enterprise Server).
6. Go back to list of secret scanning alerts. Click on the **Google API key** alert.
7. Click on **Verify secret** again. This time, it should say **secret inactive**. This is a good candidate to **Close as** --> **Revoked** (click the **Close as** button in the upper right to do so). Do this.
8. Unlike Dependabot alerts and Code Scanning alerts, secret scanning alerts are not automatically closed when the secret is removed from the code - whether by a new commit or by rewriting history. This is because the secret was exposed and you don't know who may have seen it. So, you have to manually close the alert once you revoke the token.
9. Navigate back to the **high confidence** secret alerts list.
10. We can click **1 Closed** to see the alert we just closed.
11. Click on the **Other** secret scanning alerts option. This will show all of the alerts that are not high confidence, such as generic passwords, keys, and things such as HTTP bearer authentication header tokens found in the code.
12. Let's click into one of the **Password** alerts.
13. Just like high confidence alerts, it shows where the secret was found in the code. The secret was found with AI, so it may or may not be a real secret or password. If it's not, we can close it manually and mark it as a false positive.

## Summary

Well done! You've learned how to review and triage alerts from Dependabot, code scanning, and secret scanning. And you even saw how you can use Copilot to automatically fix a code scanning alert. In the next lab, we are going to to get hands-on with code scanning, repository rulesets, and Copilot, to see how we can both prevent and fix vulnerabilities in our code base.
