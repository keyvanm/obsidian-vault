Add this to your `~/.bash_profile` or `.bashrc`
```bash
function obsidian() {
	local abs_path
	abs_path=$(realpath "$1")
	URI="obsidian://open?path=$abs_path";
	echo $URI
	open $URI
}
```
