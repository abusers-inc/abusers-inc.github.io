# DepinBot
> **Status**: Active development
## Description
Optimized multi-tasked farming of popular DePIN projects.
Has functions of:
- Registering new accounts (including verification by email)
- Farming a multitude of projects at once

## Requirements
- Appropriate captcha service and it's respective API key
- Emails with at least IMAP access
- List of usernames 
- ISP or Residential proxies. It's also possible to use DC proxies, however they are usually detected by projects

## Getting Started
First of all, you, as a user, should load accounts into database.
Each accounts acts as identity for each and every of supported projects.
This was done for ease of your's use: now each dashboard would require only one password!

This is done by setting up following three files:
1. A list of usernames. Each line is a new username. Username **can't** include spaces.
2. A list of `email:password` pairs. (e.g. `login_of_email@domain.name:password_of_email`)
3. A list of proxies in the format of: \
 `<protocol>://<username>:<password>@<ip>:<port>` \
In case proxy doesn't require authentication, you can omit whole `<username>:<password>@` part. (Note leading @ character) 

Supported proxy protocols are as following:
- `socks5`
- `socks4`
- `http` [^1] 

Next, you should decided on groups of to-be inserted accounts.
Groups are create for you to classify your accounts.
For instance, you might load accounts in different batches.
In this case, you would like to name each batch with date accounts were loaded.
If you don't want\need this functionality, you can just use `default` group name.

[^1]: This protocol assumes proxy supports TCP tunneling with HTTP CONNECT directive. Forwarding proxies (from HTTP/1.1 spec) **are not** supported!

When you are done with settings files, you should create `config.toml` file.
In this file, you specify path's to files with resources and group name:
```toml
group = "default"
emails_file = "resources/emails.txt"
proxies_file = "resources/proxies.txt"
usernames_file = "resources/usernames.txt"
```
In this case, files have been placed in one directory.

### Loading accounts
Once config is done, you can command bot to add accounts to the database.
> netsharesoft accounts add

This command requires each amount of resources to match. For example, 10 proxies = 10 usernames = 10 emails.
In case this condition doesn't hold, bot will notify it about you in the error.
Optionally, you can bypass this and other verifications conditions with `-i` (ignore) flag:
> netsharesoft accounts add -i

### Registration
Now accounts have to be registered in the services.
First of all, you need to specify which services to register, by specifying it in `config.toml`.
As of now, each project requires a list of referral codes for registration. They are specified in separate file,
and bot will select 1 ref code randomly form the list:
```toml
[[projects]]
name = "grass"
ref_codes_file = "resources/grass_refcodes.txt" # file has to exist at this location
```

Of course you can specify multiple projects, so they would register simultaneously:
```toml
[[projects]]
name = "grass"
ref_codes_file = "resources/grass_refcodes.txt" # file has to exist at this location
[[projects]]
name = "dawn"
ref_codes_file = "resources/dawn_refcodes.txt"
[[projects]]
name = "oasis"
ref_codes_file = "resources/oasis_refcodes.txt"
```
For the full list of supported projects and their instructions, please consult the table at the beggininng of this documentation.

Secondly, you have to specify captcha service. Currently with support two providers:
- Anticaptcha
- Capsolver

It's advisable to use Anticaptcha if you are planning to use Dawn functionality. Workers there solve image-based captcha much better.

In `config.toml`, write next for capsolver. In case of AntiCaptcha, replace `capsolver` with `anticaptcha`
```toml
[captcha]
captcha_service = "capsolver"
key = "CAP-XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" # Specify your key here
```

Thirdly, IMAP and/or POP3 servers of your emails have to specified.
Please consult documentation of your email provider. We can't know each and every server address beforehand.
In a nutshell, you should find **address** and **port** for one or two of the protocols.
Next, you specify them in `config.toml` like that:
```toml
[[email_servers]]
domains = ["onet.pl", "op.pl"]
imap = {domain = "imap.poczta.onet.pl", port = 993}
pop3 = {domain = "pop3.poczta.onet.pl", port = 995} # This or previous line can be ommitted,
                                                    # but at least one of them must be present

```

Lastly, command bot to start the process:
> netsharesoft exec register

### Farm!
After the registration, option to farm accounts becomes available.
To launch this process, you have to configure:
- Projects to farm
- Captcha service to use (some services might require solving while running)

The good news is that those options are compatible with last step! You don't have to change anything.

> netsharesoft exec run

Relax and watch your bags growing!
