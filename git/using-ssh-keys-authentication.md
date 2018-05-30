# Git Help
---

## Using SSH Keys for Authentication

Sometimes your git server may require you use SSH keys instead of credentials over HTTP. The URL will probably look something like this:  
`git@gitlab.com:project/REPO.git`

And whenever you try to clone, pull, or push you may see this:  
> `git@gitlab.com's password: `

When your password doesn't work, that means you need to use SSH files for authentication.

### Linux
Create and download an SSH key from your git server, `id_rsa`, then ensure ssh-agent is running and add the SSH key.

- `cp ~/Downloads/id_rsa ~/.ssh/`
- `exec ssh-agent bash`
- `ssh-add` or `ssh-add ~/.ssh/id_rsa`
> - `Identity added: /home/user/.ssh/id_rsa (/home/user/.ssh/id_rsa)`

The next time you try your git commands, it should work and not require a password.

If you get an `Could not open a connection to your authentication agent.` error after trying ssh-add, ensure that you have run ssh-agent like the second bullet point.
