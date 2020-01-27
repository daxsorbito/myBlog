---
title: "Get previous command and parameters in the terminal"
date: 2020-01-27T12:57:22+08:00
draft: false
summaryImage: "images/bash_banner.png"
tags: ["bash"]
summary: "Get previous command parameters in the terminal"
---

It always happens to me, executing a command in the terminal and only to find out that I have to do a `sudo` in executing the command or misspelled the command with a very long parameters. 

It would be ok if the command is just short, but often times it's not.

This is a bash trick to let you not retype what you've typed previously in the terminal then just to pre-pend it with `sudo`.

For example executing this command but would not allow you because you need an elevated permission to execute thus must execute it with `sudo`.
```bash
install yum docker
```
To save you some keystroke you could this.
```bash
sudo !:0 !*
```
Explanation:
  - `!:0`: this retrieves the command of the previously executed command, in this case the `install` command.
  - `!*`: this retrieves all of the parameters that was executed with the previously executed command, in this case is the `yum docker`.


Or there are times you misspelled the command itself but had a very long parameters to execute with the command. Please note the misspelled `kubclt` command.
```bash
kubclt describe po azure-vote-front-d566fffcc-m7v7h -n myownnamespace
```
To correct it, you could just do.
```bash
kubectl !*
```
Explanation:
  - `kubectl`: the correctly spelled command - to replaces the misspelled `kubctl` of the prior command.
  - `!*`: this retrieves all of the parameters that was executed with the previously executed command, in this case is the `describe po azure-vote-front-d566fffcc-m7v7h -n myownnamespace`.

So the gist of retrieving the previous command and parameter is this.
For this example
```bash
kubectl -n mynamespace port-forward deploy/azure-vote-front 8090:80
```
  - `!^`: get the first parameter, from the example about it would be `-n`.
  - `!$`: get the last parameter, from the example about it would be `8090:80`.
  - `!*`: get all of the parameters, from the example about it would be `-n mynamespace port-forward deploy/azure-vote-front 8090:80`.
  - `!:<n>`: get the `n`th index of the previously executed command. `0` would be the executed command, then `n` greater than `0` would be index of the parameters.
    - `!:0`: would be `kubectl`
    - `!:2`: would be `mynamespace`
