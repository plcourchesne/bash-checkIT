# bash-checkIT

This repos contains building blocks to track and act upon user's shift of attention; specifically to deny standby power to greedy applications - like chrome and firefox - while retaining as much functionnality as possible.


## How to install 

* sudo apt install xdotool
* backup ~/.bashrc
* add content of .bashrc.addon to ~/.bashrc
* copy file .bashrc.checkIT.lib.v1 to ~/
* run `source ~/.bashrc`

## How to use

run `checkFirefox`, toggle Firefox window.

#### Examples

Chrome to pause on blur event and to resume on focus event:
```sh
checkProcess 'chrome' 'chrome'
```

Firefox to pause 5 seconds past onblur event unless current tab title matches fond or favorite:
```sh
checkProcess 'Firefox' 'firefox' 'unless' '(fond|favorite)' 'with pause surge delays of' 5 0
```

Slack to pause 5 seconds past onblur event and to awaken for 5 seconds every 30 seconds:
```sh
checkProcess 'Slack' 'slack' 'with pause surge delays of' 5 30
```

#### Detailed usage

checkProcess __classMatcher__ __pidofNameArg__ ['unless' __titleMatcher__] ['with pause surge delays of' __pauseDelay__ __surgeDelay__]  

| Argument                 | Description |
| ----------------------   | ---------------------- |
| classMatcher             | Class matcher of targeted application, run `xprop \| grep WM_CLASS` for hint |
| pidofNameArg             | Program name for `pidof program name` to return pid of targeted application |
| titleMatcher             | Title matcher of targeted application to ignore, run `xprop \| grep WM_NAME` for hint |
| pauseDelay               | CPU cutoff delay, in seconds |
| surgeDelay               | CPU cutoff recess delay, in seconds, if greater than 0 |


## Status

Proof of concept, MVP, tested on Ubuntu.
