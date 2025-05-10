# Setting Up Multiple GitHub Accounts on Linux

Managing multiple GitHub accounts on a single Linux machine can be streamlined with the following steps:

## 1. Generate SSH Keys for Each Account
Run the following commands to create separate SSH keys for each account:
```bash
ssh-keygen -t rsa -b 4096 -C "email_for_account1@example.com" -f ~/.ssh/id_rsa_account1
ssh-keygen -t rsa -b 4096 -C "email_for_account2@example.com" -f ~/.ssh/id_rsa_account2
```

## 2. Add SSH Keys to the SSH Agent
Start the SSH agent and add the keys:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa_account1
ssh-add ~/.ssh/id_rsa_account2
```

## 3. Configure SSH Config File
Edit the `~/.ssh/config` file to define host aliases:
```plaintext
Host github-account1
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_account1

Host github-account2
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_rsa_account2
```

## 4. Clone Repositories Using Host Aliases
Use the configured host aliases to clone repositories:
```bash
git clone git@github-account1:username/repo1.git
git clone git@github-account2:username/repo2.git
```

## 5. Set Up Git Config for Each Repository
Set the appropriate user details for each repository:
```bash
cd repo1
git config user.name "Account1 Name"
git config user.email "email_for_account1@example.com"

cd ../repo2
git config user.name "Account2 Name"
git config user.email "email_for_account2@example.com"
```

## Conclusion
By following these steps, you can seamlessly manage multiple GitHub accounts on your Linux machine.