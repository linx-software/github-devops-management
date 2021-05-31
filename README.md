# GitHub - DevOps Management

## Overview

The provided sample includes:

- Generating GitHub API access tokens via OAuth 2.0.
- Authenticating and connecting to the GitHub API via Linx
- Retrieving commit activity for repositories.
- Sending email notifications from Gmail for Gitub repository commit activity for a time period. The sample Solution sends out an HTML email containing a summary of your GitHub activity from your configured Gmail account. This email can be directed to you or any others you want to alert containing the information concerning the commits you want to pass on.


---

### Additional resources

- [GitHub-Linx integration guide](https://community.linx.software/community/t/oauth-2-0-authentication-github-example/487)
- [GitHub API authentication documentation](https://docs.github.com/en/rest)
- [GitHub API documentation](https://docs.github.com/en/rest/reference/repos#list-organization-repositories)
- [Linx email configuration](https://linx.software/docs/reference/plugins/email/content/sendemail/)

---

## Dependencies

### Pre-requisites

- Linx Designer
- Github account
- Email account (*Gmail is used in this sample*)

### Linx Designer

This solution was developed in the Linx Designer `v5.21.0.0`

---

## Setting up the sample

Register a new app on GitHub:

1. Register a new 'OAuth application' on GitHub
1. Configure the 'Authorization callback URL' to be: `http://localhost:8080/oauth/token`
1. Save your app.
1. Generate your **client secret**.
1. Copy the **Client ID** and **Client Secret**.

Configure the Solution's $.Settings with GitHub details:

1. Open the solution in your Linx Designer.
1. Edit the $.Settings values:

   - `client_id`: Your GitHub app’s **Client ID**
   - `client_secret`: Your GitHub app’s **Client Secret**
   - `owner`: Insert the owner of your repository. E.g From the link https://github.com/linx-software, linx-software is the owner.

1. Save the Solution.

Generate access tokens:

1. Start the debugger on the RESTHost service in the Linx Designer.
2. Make a request in your browser to `http://localhost:8080/oauth/authorize`
3. You will be redirected to the GitHub OAuth 2.0 access consent screen.
4. Authorize the connected application.
5. View success message.

Configure the Solution's $.Settings with your email details :

> [Linx email configuration](https://linx.software/docs/reference/plugins/email/content/sendemail/) will help you get started with email plugin in Linx.

> _This sample was setup using a Gmail instance._

- `mail_username`: Username of your email account.
- `mail_password`: App password.
- `sender_mail`: Mail to use as the sender. For certain SMTP servers like GMail this defaults to yourself.
- `receiver_mail`: Mail address of 'To' for notification email.

---


## Using the sample

### Authentication

After your app has been successfully authorized, the access token is stored in a local text file.

Requests are authenticated via a Bearer access token included in the `Authorization` header of each request.

The token is retrieved from the file before each request is made.

### Making requests

When making requests to the GitHub, you must also include the following header:

```http
User-Agent: Mozilla/5.0 (Windows NT 6.1) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/47.0.2526.111 YaBrowser/16.3.0.7146 Yowser/2.5 Safari/537.36
```

---

## Utilities samples

### GetReposForOwner

[Lists repositories](https://docs.github.com/en/rest/reference/repos#list-organization-repositories) for the specified organization.

### GetCommits

The [Repo Commits API](https://docs.github.com/en/rest/reference/repos#list-commits) supports listing, viewing, and comparing commits in a repository.

Parameters:

| Parameter | Type          |                                                                                                                     |
| --------- | ------------- | ------------------------------------------------------------------------------------------------------------------- |
| repo      | string query  | Repositories' name                                                                                                  |
| since     | string query  | Only show notifications updated after the given time. This is a timestamp in ISO 8601 format: YYYY-MM-DDTHH:MM:SSZ. |
| until     | string query  | Only commits before this date will be returned. This is a timestamp in ISO 8601 format: YYYY-MM-DDTHH:MM:SSZ.       |
| per_page  | integer query | Results per page (max 100). Default: 30.                                                                            |

### MailCommitForRepo

The function uses the repositories' list and commit list from the above function and mail the commit details to the recipient.

Parameters:

- `per_page`: integer query. Results per page (max 100)
- `since`: start date of commits (e.g Yesterday's date or any other date before ‘until date below’: 2021-05-26)
- `until`: end date of commits (e.g Today's date : 2021-05-27)

## Running the Sample

Click on the function named RUN
Enter parameters as follows:

- `Per_page`: 1
- `Since`: start date of commits (e.g Yesterday's date or any other date before ‘until date below’: 2021-05-26)
- `Until`: end date of commits (e.g Today's date : 2021-05-27)
