### Travis CI stuffs

#### How to integrate with GitHub pages?

1. Go to https://travis-ci.com/ and verify your repo

2. Create a personal access token

Create a token with what to grant:
https://github.com/settings/tokens

https://help.github.com/en/github/authenticating-to-github/creating-a-personal-access-token-for-the-command-line

3. Set GITHUB_TOKEN in Travis environment variables

![Environment variable](https://github.com/manoaman/til/blob/master/travis/Screen%20Shot%202020-03-26%20at%206.22.17%20PM.png)


#### Differenece between travis-ci.org and travis-ci.com?

> Travis CI originally created two separated platforms to differentiate between private repos / paid (travis-ci.com) and public repos / free (travis-ci.org).

> However, as of May 2018, new users and projects (both private and public) should only use travis-ci.com (see official announcement):

https://devops.stackexchange.com/questions/1201/whats-the-difference-between-travis-ci-org-and-travis-ci-com
