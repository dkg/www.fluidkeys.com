---
title: "Send encrypted secrets from the command-line: Fluidkeys v0.3"
description: With Fluidkeys 0.3 you can send passwords, keys, tokens and personal data to team-mates using end-to-end encryption.
author: Paul Fawkesley & Ian Drysdale
date: 2019-01-08
---

Today we proudly announce Fluidkeys 0.3 😄

With Fluidkeys v0.3 you can send passwords, keys, tokens and personal data to team-mates using end-to-end encryption.

![Terminal showing sending a secret token to a team-mate](/images/release-0-3-send-secret.svg)

If you're keen to get started, head to [download.fluidkeys.com](https://download.fluidkeys.com)

## Sharing passwords, tokens, credentials and keys

From listening to engineering teams, we heard a number of different types of sensitive information with similar characteristics:

* **Names and addresses** of customers [(PII)](https://en.wikipedia.org/wiki/Personally_identifiable_information) shared with other internal teams
* **API access tokens** sent to external developer partners
* **SSH key pairs** for Amazon EC2 shared with freelance developers
* **IAM credentials** for Amazon Web Services
* **Temporary passwords** sent to new team members
* **PGP private keys** for shared mailboxes
* **Encryption passwords** for encrypted ZIP files

These are small bits of text, fairly short lived, with a potentially high impact if breached (like a [$50,000 Amazon bill](https://www.quora.com/My-AWS-account-was-hacked-and-I-have-a-50-000-bill-how-can-I-reduce-the-amount-I-need-to-pay))

### How to quickly share throwaway secrets?

You've got stuff to do, you need to get this thing sent, what are you going to do?

The easy route is to throw it into Slack and hope they aren't next week's big data breach.

Maybe you could use a messaging app like WhatsApp or Signal. But that requires you know your team-mate's number, which isn't the norm for many teams. And WhatsApp is determined to back itself up to Google Drive, so it'll probably end up there too.

You could use GPG, but can you remember the command? And do you have the other person's public key? And are you confident that they'll copy-paste the funny text correctly on their end?

<pre>
<span class="prompt">$</span> gpg --armor --recipient paul@fluidkeys.com --encrypt
-----BEGIN PGP MESSAGE-----

hQEMA35uuyjbagYuAQf/eqfq3MCS96ZNNQeI7S3zGs7FiAIiQ7qU5Oa1Dz6/UizC
pQnTHjoupyGChXeDz9XDdmWtTuvYArlnjdVJfySHWGDQ66mm/IUie0jsnTOss6P1
...
</pre>

You could put it in your shared password manager, but it's a bit overkill since you only need to send it once, and sometimes you see a delay on shared items showing up.

### Send encrypted secrets from the command-line

With Fluidkeys you can send PGP-encrypted secrets directly from the command-line using your team-mate's email address.

<pre class="terminal">
<span class="prompt">$</span> fk secret send paul@fluidkeys.com
</pre>

## Fluidkeys fetches verified public keys automatically

When you install and set up Fluidkeys, you're asked for your email address. Once you've verified it, others can send you secrets. You don't need to manually exchange public keys.

Fluidkeys automatically fetches keys based on the verified email address and encrypts the secret to the key.

<pre class="terminal">
<span class="prompt">$</span> fk secret send paul@fluidkeys.com
<span class="positive"> ▸   Found public key for paul@paulfurley.com</span>
</pre>

We use [our own server](https://github.com/fluidkeys/api) to store public keys and transmit encrypted secrets.

## Install and set up Fluidkeys in 2 minutes

We've heard from a number of teams that it's time consuming to set up new starters with PGP and we've worked hard on this.

It takes around 2 minutes for new users to install Fluidkeys, generate a PGP key, verify your email and start sending and receiving encrypted secrets.

[Take the two-minute challenge](https://download.fluidkeys.com)

## Things to be aware of

### Fluidkeys stores your keys in gpg

Beware that Fluidkeys doesn't implement its own storage of keys: it stores them in `gpg`. If you delete a key from `gpg`, there's no copy in Fluidkeys. We don't modify the `GNUPGHOME` directory: we push and pull straight from your default `gpg2` installation.

This is helpful if you use your keys for anything else like signing commits with `git` or encrypted email with Thunderbird.

Those applications will use keys made by Fluidkeys, and Fluidkeys will keep them updated.

### Fluidkeys stores your key's password in your system keychain

In order to be able to rotate your key automatically, Fluidkeys stores the password to your private key in your system keychain. You can see these by searching for "Fluidkeys".

### Fluidkeys doesn't upload to the public keyserver network

We chose not to use the public keyserver network until it supports deleting keys and cryptographic validation.

If you do want to upload to the public keyservers, make sure you automate it. Because Fluidkeys automatically rotates your encryption subkey every month, your key will quickly become out of sync with the keyservers. You could add cron task to upload your key regularly:

Edit your crontab by running `crontab -e` and add this line:

```
@daily gpg --keyserver pool.sks-keyservers.net --send-key <email address>
```

## Download Fluidkeys v0.3

On to business: head on over to [download.fluidkeys.com](https://download.fluidkeys.com) to get started.

<pre class="terminal">
<span class="prompt">$</span> fk --help
Fluidkeys 0.3.0

Configuration file: /home/paul/.config/fluidkeys/config.toml

Usage:
    fk setup
    fk setup &lt;email&gt;
    fk secret send &lt;recipient-email-address&gt;
    fk secret receive
    fk key create
    fk key from-gpg
    fk key list
    fk key maintain [--dry-run]
    fk key maintain automatic [--cron-output]
    fk key upload

Options:
    -h --help         Show this screen
       --dry-run      Don't change anything: only output what would happen
       --cron-output  Only print output on errors

</pre>

## What do you think?

Please have a go and let us know how you get on!

We're excited to hear from you :)

— Paul & Ian

[Email hello@fluidkeys.com](mailto:hello@fluidkeys.com)
