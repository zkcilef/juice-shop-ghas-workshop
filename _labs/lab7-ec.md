# Extra Credit - Lab 7 - Advanced CodeQL Setup

We set up Code Scanning with CodeQL using the default method. Now, let's try using the **[advanced setup](https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/configuring-advanced-setup-for-code-scanning)**!

This extra credit lab covers parts of the following exam domains:

- Domain 4: Configure and use code scanning
- Domain 5: Use code scanning with CodeQL
- Domain 6: Describe GitHub Advanced Security best practices

## Exercise

Why might you want to use the advanced setup? Here are some reasons:

- More control over triggers and schedule
- When pulling in packages from a private feed, you may have to provide instructions on authorizing to the NuGet, NPM, Maven, etc. feed.
- For compiled languages, providing more instructions on how to build the code
- Ability to customize your runners TODO: is this true? i think you can use code-scanning label with default workflow but i cannot remember
- Ability to customize the CodeQL configuration (such as query suites used)
- Manage code scanning settings "as code"
- Utilize 3rd party code scanning tooling

### Assignment

Your assignment here is to switch to the **[advanced setup](https://docs.github.com/en/code-security/code-scanning/creating-an-advanced-setup-for-code-scanning/configuring-advanced-setup-for-code-scanning)**. You can start under the **Settings** --> **Code Security and Analysis** page.

Your goal is to have a CodeQL workflow committed that successfully scans your code. Pay attention to some of the configuration options for the CodeQL scanning action. Refer to the documentation for more details.

TODO: add link

## Summary

TODO: add content

➡️ Head back to the [labs](README.md) page.