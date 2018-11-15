# New Macbook developer environment setup

## Terminal
- Install [iTerm](https://www.iterm2.com/)
- Update preferences/profile:
	- Set `General > Name`
	- Set `Colors > Basic Colors > Foreground` to `66b400`
	- Set `Colors > Basic Colors > Selection` to `3196e0`
	- Set `Colors > Basic Colors > Selected text` to `f4fb86`
	- Toggle `Text > Blinking cursor`
	- Set `Text > Font` to `13pt Andale Mono`, `use a different font for non-ASCII text` to `checked`, and toggle `anti-aliased`
	- Set `Text > Non-ASCII Font` to `12pt Monaco` and toggle `anti-aliased`
	- Toggle `Window > Blur` to ~15%
	- Set `Terminal > Scrollback lines` to `10,000`
	- Toggle `Session > Always prompt before closing`

## Text editor
- Install [SublimeText](https://www.sublimetext.com/)
- Create `subl` command via simlink
	- `ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/subl`
- Install [Package Control](https://packagecontrol.io/installation)
	- Install Babel
	- Install GitGutter
	- Install MarkdownPreview
	- Install Materialize
	- Install Sass
	- Install SideBarEnhancements
	- Install TypeScript
- Update SublimeText preferences:
	- Hold `command` and press `,` to open preferences
	- Edit "Users" preferences file (should open in right-most pane... saves to `/Users/USER_NAME/Library/Application\ Support/Sublime\ Text\ 3/Packages/User/Preferences.sublime-settings`:
```json
{
	"binary_file_patterns":
	[
		"*.dds",
		"*.eot",
		"*.gif",
		"*.ico",
		"*.jar",
		"*.jpeg",
		"*.jpg",
		"*.pdf",
		"*.png",
		"*.swf",
		"*.tga",
		"*.ttf",
		"*.zip",
		"node_modules/**"
	],
	"color_scheme": "Packages/Babel/Monokai Phoenix.tmTheme",
	"default_line_ending": "unix",
	"ensure_newline_at_eof_on_save": true,
	"font_size": 13,
	"git_gutter_show_line_annotation": false,
	"highlight_modified_tabs": true,
	"ignored_packages":
	[
		"Vintage"
	],
	"tab_size": 2,
	"theme": "Material Monokai.sublime-theme",
	"translate_tabs_to_spaces": true,
	"trim_trailing_white_space_on_save": true
}
```

## XCODE
- Install [XCODE CLI tools](https://www.google.com/search?q=xcode+cli+tools+install&oq=xcode+cli+tools&aqs=chrome.0.0j69i57j0l4.2785j0j7&sourceid=chrome&ie=UTF-8)
	- `xcode-select --install`

## Homebrew
- Install [Homerew](https://brew.sh/) package manager
	- `ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

## ZSH
- Optionally install latest version of [ZSH](http://www.zsh.org/) with Homebrew:
	- `brew install zsh`
	- `echo /usr/local/bin/zsh >> /etc/shells`
- Set ZSH as default shell:
	- `chsh -s $(which zsh)` (`chsh -s /bin/zsh` to use OS version, `chsh -s /usr/local/bin/zsh` to use Homebrew version)
- Install [Prezto](https://github.com/sorin-ionescu/prezto)
	- `git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"`
	- Run:
```
setopt EXTENDED_GLOB
for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
	ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
done
```

## Node
- Install [Node.js](https://nodejs.org/en/)
	- `brew install node`
- Install [Node Version Manager](https://github.com/creationix/nvm)
	- `brew install nvm`
	- `mkdir ~/.nvm`
	- Append to `.zshrc` (or `/Users/USER_NAME/.zprezto/runcoms/zshrc`):
```
# Add nvm env vars
export NVM_DIR="$HOME/.nvm"
. "$(brew --prefix nvm)/nvm.sh"
```

	- `nvm install node`
	- `nvm install --lts`
	- `nvm use node`
	- `nvm run node --version`
	

## Git
- Install [Git](https://git-scm.com/)

## Gitconfig
- Update `.gitconfig` in `$HOME` (`/Users/USER_NAME`) directory:
```
[user]
  email = GITHUB_USER_NAME@users.noreply.github.com
  name = GITHUB_USER_NAME

[core]
  editor = nano
  excludesfile = /Users/USER_NAME/.gitignore_global

[merge]
  summary=true

[color]
  ui = auto

[color "branch"]
  current = yellow reverse
  local = yellow
  remote = green

[color "diff"]
  meta = yellow bold
  frag = magenta bold
  old = red bold
  new = green bold

[color "status"]
  added = yellow
  changed = green
  untracked = cyan

[alias]
  st = status
  ci = commit
  br = branch
  co = checkout
  df = diff
  lg = log -p
  gl = log --graph --decorate --pretty=oneline --abbrev-commit
  gla = log --graph --decorate --pretty=oneline --abbrev-commit --all
  ls = ls-files
  dtag = tag release-`date "+%Y%m%d%H%M"`
  unstage = reset HEAD
  uncommit = reset --soft HEAD^
  wc = whatchanged -p --abbrev-commit --pretty=medium
[push]
  default = simple
```
also, optionally add:
```
[difftool "sourcetree"]
	cmd = opendiff \"$LOCAL\" \"$REMOTE\"
	path = 
[mergetool "sourcetree"]
	cmd = /Applications/SourceTree.app/Contents/Resources/opendiff-w.sh \"$LOCAL\" \"$REMOTE\" -ancestor \"$BASE\" -merge \"$MERGED\"
	trustExitCode = true
```
- Update `.gitignore_global`:
```
*~
.DS_Store
```

# NPM Token
- Get [NPM token](https://docs.npmjs.com/creating-and-viewing-authentication-tokens)
	- `npm login`
	- `subl ~/.npmrc` and copy value assigned to `//registry.npmjs.org/:_authToken=`
- Update `.bash_profile` in  in `$HOME` (`/Users/USER_NAME`) directory:
```
export NPM_TOKEN="YOUR_NPM_TOKEN"
```
replacing "YOUR_NPM_TOKEN" with the value copied from `~/.npmrc`.

## Git Flow
- Install [Git Flow](https://github.com/nvie/gitflow)
- `brew install git-flow`

## Yarn
- Install [Yarn](https://yarnpkg.com)
	- `brew install yarn --without-node` or `brew install yarn` if not using `nvm`

## Misc packages 
Primary examples: `openssl`, `readline`, `jq`.
Also check for: `gnu-sed`, `xz`, `libxml2`, `autoconf`, `icu4c`, `pkg-config`, `sqlite`, `rbenv`, `gdbm`
```sh
brew install openssl
brew install readline
...
```

## Docker
- Install [Docker](https://www.docker.com/)

## Postgres
- Install [Postgres](https://www.postgresql.org/)
	- `brew install postgresql` or [download binary](https://www.postgresql.org/download/)

## Install applications
- [Chrome](https://www.google.com/chrome)
- [Firefox](https://www.mozilla.org/en-US/firefox/new)
- [Opera](https://www.opera.com)
- [SourceTree](https://www.sourcetreeapp.com)
- [PSequel](http://www.psequel.com)
- [VLC](https://www.videolan.org/vlc/index.html)
- [Slack](https://slack.com)
- [Spotify](https://www.spotify.com/)
- [1Password](https://1password.com/)

## Heroku CLI
- [Install Heroku CLI tools](https://devcenter.heroku.com/articles/heroku-cli)
	- `brew install heroku/brew/heroku`
	- If `which heroku` returns `heroku: aliased to nocorrect heroku` then append to `~/.zshrc`:
```
unalias heroku
```

## Algolia CLI
- [Install Algolia CLI tools](https://github.com/algolia/algolia-cli)
	- `npm i -g @algolia/cli`

## JQ CLI
- Install [jq](https://stedolan.github.io/jq/) command-line JSON processor
	- `brew install jq`
