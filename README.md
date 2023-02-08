# About

A shell function for auto-completing script commnds from package.json.

# Installation

1. Install jq and fzf (`sudo apt install jq fzf`)
2. Copy this one line function to your ~/.bashrc or ~/.zshrc (`source ~/.bashrc` or `source ~/.zshrc` to refresh in-place).
   You can also just copy-paste this into your terminal to play with it.

```shell
function ppp(){ pnpm $(jq -r ".scripts|keys[]"<$(npm root|sed 's/node_modules//')package.json|fzf -q "$1" );};
```
This uses `pnpm` - if you're using yarn or npm replace pnpm in the function with yarn or npm.

# Usage

Using [this package.json](https://github.com/0xProject/tools/blob/development/package.json) as an example:

```shell
$ ppp t
```

<img width="410" alt="image" src="https://user-images.githubusercontent.com/84268/217463783-8f0c5b39-624a-443f-ae9b-082997030ee4.png">

# Other Uses

You can extend this for any pattern of "execute-command against result of fuzzy search against something".

For example, this shell function adds a command `hi` which you can run alone or type `hi <first few letters>`. It searches a dictionary and echo's "Your word is: <word>"

```shell
function hi(){ echo "Your word is: $(cat /usr/share/dict/words | fzf -q "$1" --prompt "hi> ")";};
```

 <img width="262" alt="image" src="https://user-images.githubusercontent.com/84268/217465082-9dac39cd-7b0b-4f3b-9bce-03b5b5968216.png">

```shell
Your word is: worldliness
```

fzf also has an argment for executing a command against results: `--bind "enter:execute(less {})"`, but this runs the command then brings you back int fzf.
