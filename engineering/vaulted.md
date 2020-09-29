<!-- TITLE: Vaulted -->
<!-- SUBTITLE: How to use Vaulted for AWS secrets -->

# Vaulted

## Overview
Vaulted is a tool to securely store secrets and spawn environments with them available.
See the documentation here: https://github.com/miquella/vaulted
It's a good tool to use to store AWS access keys.

## Creating a new vault
1. `brew install vaulted`
1. `vaulted add name-of-vault` (ex: `vaulted add neighbor`)
1. `a` (to edit the AWS Key)
1. `k` (to add the key)
	* paste in your AWS Key ID
	* paste in your AWS Key Secret
1. `t` (to toggle "Substitute with temporary credentials" to false.  We aren't set up to support this.)
1. `b` (to go back to the previous menu)
1. `d` (to edit the duration the shell lives for)
	* enter the time you want your shells to live for (ex: `24h`)
1. `q` (to save and quit)
	* enter a password to be used to spawn the shell
	* confirm the password

## Spawning a shell
Now when you want to do things that require access to AWS, you can spawn a Vaulted shell to have your access keys loaded in.
1. `vaulted shell name-of-vault`
1. enter the password
You are now in a vaulted shell and can do things that require AWS access
(e.g. start the app with the ./setup.sh script)
The shell will live for the duration you specified.  At that point, exit the shell (`exit`) and restart it